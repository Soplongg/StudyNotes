1. ArrayList底层是由数组实现的，LinkedList底层是由链表实现的。
2. ArrayList更擅长随机访问，LinkedList更擅长与添加删除。
3. 二者都实现了List接口，LinkedList还实现了Queue接口，可以当做队列使用。ArrayList实现了RandomAccess接口，支持随机访问也就是按数组下标访问。
4. ArrayList在add( )的时候会扩容,如果指定位置,会因为需要移动其他元素的位置导致时间复杂度上升。LinkedList只需要插入节点即可。