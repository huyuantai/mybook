1) For synchronization block. How

   synchronize(this){
    // code
   }
differs from

   synchronize(MyClass.class){
    //code
   }
   


this - is the reference to particular this instance of class, 

MyClass.class - is the reference to MyClass description object.

此同步块的不同之处在于，第一个将同步与MyC类实例具体地处理的所有线程，
而第二个线程将同步所有线程，而独立于调用该方法的对象