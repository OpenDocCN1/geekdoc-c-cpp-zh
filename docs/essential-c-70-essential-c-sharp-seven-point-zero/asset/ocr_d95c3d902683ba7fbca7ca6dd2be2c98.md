```
Console.SetCursorPosition(
		currentPosition.X, currentPosition.Y);

		Undo();
	}
	break;

	case ConsoleKey.DownArrow:
	case ConsoleKey.UpArrow:
	case ConsoleKey.LeftArrow:
	case ConsoleKey.RightArrow:
		// SaveState()
		currentPosition = new Cell(
			Console.CursorLeft, Console.CursorTop);
		// Only type Cell allowed in call to Push()
		path.Push(currentPosition);
		break;

	default:
		Console.Beep(); // Added in C# 2.0
		break;
	}
	} while (key.Key != ConsoleKey.X); // Use X to quit
}
```

The results of Listing 12.6 appear in Output 12.2.

# **OUTPUT 12.2**

![](bbox=[0.15, 0.6, 0.69, 0.89])