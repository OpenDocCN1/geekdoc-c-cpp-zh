# Class’s Threading Model Key

| Creator's Apartment Model | Class's Threading Model Key |  |  |  |  |  |
|---|---|---|---|---|---|---|
|  |  | Apartment | Free | Both | Neutral | Not Specified |
| Single-Threaded | Not “Main” | Created in Current Apartment | Created in Multi-Threaded Apartment | Created in Current Apartment | Created in Neutral Apartment | Created in “Main” Single-Threaded Apartment |
| Single-Threaded | “Main” | Created in Current Apartment | Created in Multi-Threaded Apartment | Created in Current Apartment | Created in Neutral Apartment | Created in Current Apartment |
| Multi-Threaded |  | Created in “Host” Single-Threaded Apartment | Created in Multi-Threaded Apartment | Created in Multi-Threaded Apartment | Created in Neutral Apartment | Created in “Main” Single-Threaded Apartment |
| Neutral (on STA Thread) |  | Created in Single-Threaded Apartment for this thread | Created in Multi-Threaded Apartment | Created in Neutral Apartment | Created in Neutral Apartment | Created in “Main” Single-Threaded Apartment |
| Neutral (on MTA Thread) |  | Created in “Host” Single-Threaded Apartment | Created in Multi-Threaded Apartment | Created in Neutral Apartment | Created in Neutral Apartment | Created in “Main” Single-Threaded Apartment |