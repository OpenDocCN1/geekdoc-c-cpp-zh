```
printf("-- Poly Pressure Ch:%d Note:%d Value:%d \n", uChannel, (UINT)data11,
(UINT)data2);
#endif
```

```
break;
```

```
}
```

```
case PROGRAM_CHANGE:
```

```
{
```

```
#ifdef LOG_MIDI
printf("-- Program Change Num Ch:%d Value:%d \n", uChannel, (UINT)data11);
#endif
```

```
break;
```

```
}
```

```
case CHANNEL_PRESSURE:
```

```
{
```

```
#ifdef LOG_MIDI
printf("-- Channel Pressure Value:%d Value:%d \n", uChannel, (UINT)data11);
#endif
```

```
break;
```

```
}
```

```
// --- call base class to do it its thing
```

```
return AUMIDIBase::HandleMidiEvent(status, channel, data1, data2,
inStartFrame);
```

```
}
```