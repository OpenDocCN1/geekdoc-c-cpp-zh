# (FIGURE 14.10 continued)

```
void pond_week(vector<herbivore>& fish, vector<plant>& weeds)
{
    // Variables for an index and an iterator for the weeds:
    vector<plant>::iterator      wi;
    vector<plant>::size_type     weed_index;

    // Variables for an index, an iterator, and counters for the fish:
    vector<herbivore>::iterator  fi;
    vector<herbivore>::size_type fish_index;
    vector<herbivore>::size_type new_fish_population;

    size_t many_iterations; // How many random nibbles to simulate
    size_t i;               // Loop counter

    // Have randomly selected fish nibble on randomly selected plants.
    many_iterations = AVERAGE_NIBBLES * fish.size();
    for (i = 0; i < many_iterations; ++i)
    {
        fish_index = rand() % fish.size(); // Index of a random fish
        weed_index = rand() % weeds.size(); // Index of a random weed
        fish[fish_index].nibble(weeds[weed_index]);
    }

    // Simulate the weeks for the weeds.
    for (wi = weeds.begin(); wi != weeds.end(); ++wi)
        wi->simulate_week();

    // Simulate the weeks for the fish, and count how many died.
    fi = fish.begin();
    while (fi != fish.end())
    {
        fi->simulate_week();
        if (!(fi->is_alive()))
            fish.erase(fi);
        else
            ++fi;
    }

    // Calculate the new number of fish, and reset the fish vector to this size.
    // If this adds new fish to the vector, then those new fish will be equal to the
    // SAMPLE_FISH that is used for all of our fish:
    new_fish_population = (1 + BIRTH_RATE) * fish.size();
    fish.resize(new_fish_population, SAMPLE_FISH);
}
```