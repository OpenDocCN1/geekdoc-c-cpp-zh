```
			color_menu.hide();
			attach(menu_button);
			attach(lines);
		}
```

Note that the initializers are in the same order as the data member definitions. That’s the proper order in which to write the initializers. In fact, member initializers are always executed in the order their data members were declared. Some compilers (helpfully) give a warning if a base or member constructor is specified out of order.

# ## 16.8 Debugging GUI code

Once a GUI program starts working it is often quite easy to debug: what you see is what you get. However, there is often a most frustrating period before the first shapes and widgets start appearing in a window or even before a window appears on the screen. Try this `main()`:

```
int main()
{
    Lines_window {Point{100,100},600,400,"lines"};
    return gui_main();
}
```

Do you see the error? Whether you see it or not, you should try it; the program will compile and run, but instead of the `Lines_window` giving you a chance to draw lines, you get at most a flicker on the screen. How do you find errors in such a program?

+   - By carefully using well-tried program parts (classes, function, libraries)
- By simplifying all new code, by slowly "growing" a program from its simplest version, by carefully looking over the code line by line
- By checking all linker settings
- By comparing the code to already working programs
- By explaining the code to a friend

The one thing that you will find it hard to do is to trace the execution of the code. If you have learned to use a debugger, you have a chance, but just inserting "output statements" will not work in this case – the problem is that no output appears. Even debuggers will have problems because there are several things going on at once ("multi-threading") – your code is not the only code trying to interact with the screen. Simplification of the code and a systematic approach to understanding the code are key.