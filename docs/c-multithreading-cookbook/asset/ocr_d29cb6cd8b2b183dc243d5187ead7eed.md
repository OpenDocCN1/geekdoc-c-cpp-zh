# Chapter 6

this->Controls->Add( label );
this->Controls->Add( progress );

Now, it is time to create our thread (task). As in the native approach, we must specify its start address, if needed, we pass an argument to its starting routine. As our start routine is marked static, we will pass the pointer to the routine in order to use our class instance. The task constructor expects a pointer to the Action object, and if the Action<Object>* is overloaded, it also expects a parameter constructor. We will create a pointer to Action<Object>* as follows:

```
gcnew new Action<Object>*( &MyForm::StartAddress )
```

The Action constructor explains the delegate (function pointer) to pass on, and we are providing the address of the StartAddress method.

Now, let's explain the StartAddress method. First, we need to instantiate a delegate that will later be used for invoking the main thread (similar to void*); next, we will instantiate a delegate that will be used for invoking the main thread to update the progress bar. This is very important to understand! Unlike the native approach, CLR pays attention to which thread creates what, and only the thread that created a control can manipulate it. As the main thread has created the progress bar in the Initialize method the main thread can manipulate it. If you try to update the progress bar from another thread, you'll get an error Cross-thread operation not valid: Control 'progress' accessed from a thread other than the thread it was created on. In other words, the working thread has to ask the main thread to update it, because the main thread created the progress bar. This can be achieved using the Invoke and BeginInvoke methods. These two methods are doing the same thing; they execute a delegate on the thread that controls the underlying handle was created. The difference between them is that BeginInvoke does asynchronously, while Invoke does that by waiting for the operation to return. Then, we will need to iterate n times, and at the end of each iteration we will call BeginInvoke to update the progress bar. After the iterations completed, we will perform the same task for setting the label text.

As we said earlier, we will instantiate a delegate for both the previously described operations. In order to achieve that, we must declare delegates and methods to be invoked. The declarations are shown in the following code:

```
delegate void UpdateProgressBarDelegate( void );
System::Void UpdateProgressBar( void )
{
    progress->PerformStep();
}
```

241