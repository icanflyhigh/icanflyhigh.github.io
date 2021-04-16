---
layout:     post
title:      c++_map_find_iterator类型的问题
subtitle:   学习
date:       2021-04-15
author:     simplex
header-img: img/page_back.jpg
catalog: true
tags:
    - 日常 
    - 学习
---

# c++_map_find_iterator类型的问题

在写软件课设的时候遇到的一个问题，

```c++
enum node_type {
	node_nop,
	node_assign,
	node_add, 
	node_sub, 
	node_mul, 
	node_div, 
	node_if, 
	node_while, 
	node_declare,
};

map<string, node_type>  node_type_map {
	{{"nop"}, node_nop},
	{{"assign"}, node_assign},
	{{"add"}, node_add},
	{{"sub"}, node_sub},
	{{"mul"}, node_mul},
	{{"div"}, node_div},
	{{"if"}, node_if},
	{{"while"}, node_while},
	{{"declare"}, node_declare,}
};
node_type check_node_type(const string & s) 
{
	map<string, node_type>::iterator iter = node_type_map.find(s);
    //VS在上面那句话报错
    /*
    严重性	代码	说明	项目	文件	行	禁止显示状态
错误(活动)	E0312	不存在用户定义的从 "std::_Tree_const_iterator<std::_Tree_val<std::conditional_t<true, std::_Tree_simple_types<std::pair<const std::string, node_type>>, std::_Tree_iter_types<std::pair<const std::string, node_type>, size_t, ptrdiff_t, std::pair<const std::string, node_type> *, const std::pair<const std::string, node_type> *, std::pair<const std::string, node_type> &, const std::pair<const std::string, node_type> &, std::_Tree_node<std::pair<const std::string, node_type>, void *> *>>>>" 到 "std::conditional_t<false, std::_Tree_const_iterator<std::_Tree_val<std::conditional_t<true, std::_Tree_simple_types<std::pair<const std::string, node_type>>, std::_Tree_iter_types<std::pair<const std::string, node_type>, size_t, ptrdiff_t, std::pair<const std::string, node_type> *, const std::pair<const std::string, node_type> *, std::pair<const std::string, node_type> &, const std::pair<const std::string, node_type> &, std::_Tree_node<std::pair<const std::string, node_type>, void *> *>>>>, std::_Tree_iterator<std::_Tree_val<std::conditional_t<true, std::_Tree_simple_types<std::pair<const std::string, node_type>>, std::_Tree_iter_types<std::pair<const std::string, node_type>, size_t, ptrdiff_t, std::pair<const std::string, node_type> *, const std::pair<const std::string, node_type> *, std::pair<const std::string, node_type> &, const std::pair<const std::string, node_type> &, std::_Tree_node<std::pair<const std::string, node_type>, void *> *>>>>>" 的适当转换	simple_compiler	
    */
	if ( iter == node_type_map.end())return node_nop;
	return (*iter).second;
}
```

问题：类型转化的问题，我在我上找了半个小时，真的没找的，因为报错太长了，我无法描述

最后自己解决了

```c++
// map<string, node_type>::iterator iter = node_type_map.find(s);改为
auto iter = node_type_map.find(s);
// 因为map<string, node_type>::iterator 无法转化为相应的类型
```

希望遇到同样问题的你能够看见

## 总结

以后iterator 要用auto， 多香啊



这个bug，第一次真的，让我生气了

我怎么能这么沙口

