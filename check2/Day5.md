day 5
姓名： 党聪
学习时间：2019 7 20
学习内容： 
1、理解注释https://github.com/python/cpython/blob/master/Tools/demo 中的eiffel.py
学习用时： 50 min
学习心得：

import unittest
from types import FunctionType as function
# 一个继承了type类的类
class EiffelBaseMetaClass(type):
    def __new__(meta, name, bases, dict):
        meta.convert_methods(dict)
        return super(EiffelBaseMetaClass, meta).__new__(
            meta, name, bases, dict)

# 直接可以用类名来调用的方法的修饰符，俗称类方法
    @classmethod
    def convert_methods(cls, dict):
        """Replace functions in dict with EiffelMethod wrappers.
        The dict is modified in place.
         If a methodends in _pre or _post, it is removed from the dict
        regardless of whether there is a corresponding method.
        """
        # find methods with pre or post conditions
        methods = []

        # 这里可以看出来dict里面是什么: {"%s_pre": type(###)}相当于是一个注明函数名称和类型字典
        for k, v in dict.items():
    #  在字典中找到以pre或者post结尾的键
            if k.endswith('_pre') or k.endswith('_post'):
                # 判断键对应的值是否是function类，如果键关键字的尾部包含这两个字符串，则断言v是函数类
                assert isinstance(v, function)
            # 否则再次判断v是否是function类    
            elif isinstance(v, function):
                # 如果名称里面不含pre和post，且属于function，则添加进method列表中
                methods.append(k)
        #  遍历得到的列表       
        for m in methods:
            
            # 把method中原本不是以pre或者post结尾的key拿出来，装上pre和post，
            # 再判断，也就是说判断dict的键里面是否有这样两个字符串, ##_pre 和 ##
            pre = dict.get("%s_pre" % m)
            post = dict.get("%s_post" % m)
            #如果dict的键里有一个匹配了##_pre或者##_post 
            if pre or post:
        # 这里不明白cls是什么鬼，为什么可以调用make_eiffel_method
                # 把查询到的方法pre，post带入这个函数，意味着dict里key m 对应的方法被替换掉了
                dict[m] = cls.make_eiffel_method(dict[m], pre, post)
 
# 继承了EiffelBaseMetaClass的类 EiffelMetaClass1，所以父类的类方法子类可以用吗？
class EiffelMetaClass1(EiffelBaseMetaClass):
    # an implementation of the "eiffel" meta class that uses nested functions
# 静态方法
    @staticmethod
    def make_eiffel_method(func, pre, post):
        def method(self, *args, **kwargs):
            if pre:
# pre = dict[m_pre] 而func = dict[m]
                pre(self, *args, **kwargs)
            rv = func(self, *args, **kwargs)
            if post:
                post(self, rv, *args, **kwargs)
            return rv
# __doc__，用于描述该对象的作用。
        if func.__doc__:
最终用dict[m]的描述置换method的描述
            method.__doc__ = func.__doc__

        return method
