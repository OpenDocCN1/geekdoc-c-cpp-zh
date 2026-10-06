
# Supply Chain Challenges

Describe how Apple's supply chain works. What challenges do we face on a day-to-day basis?

### Things to Consider

How does Apple accurately predict vendor performance, such as ability to meet production targets and maintain quality standards, given that Apple's specifications are often unique?

### Common Mistakes

Missing out on any of the most common supply chain challenges including:

- Challenges in forecasting customer demand
- Meeting customer expectations around quality and service
- Rising transportation costs
- Global competition
- Rising commodity prices
- Growing customer requirements
- Financial fluctuations like foreign currency risk
- Challenges with recruiting and retaining talent
- Long lead times
- Executive mandates to cuts costs
- Inability to deal with complexity effectively

# Answer

CANDIDATE: I would imagine Apple works with a lot of hardware manufacturers for iPhones, iPads, and Macs. Most of these are probably in Asia, and there are tons of different manufacturers. Foxconn is a big one, but I would imagine Apple works with a lot of different hardware manufacturers for different parts.

- **Syncing Up.** There will be a lot of syncing between manufacturers. So let say the iPhone parts A, B, and C. If all three parts are from different manufacturers, I would imagine we would need to make sure they are synced on production amounts and progress. In scenarios where a certain part is needed more than the other, we would need to coordinate that too. This happens if we need parts for repairs as well.
- **Keeping Count.** We need to make sure X number of parts are produced every day to meet demand. This would probably change on a daily basis based on sales figures. We would also do a lot of preemptive work, such as making we churn out more parts with a holiday closing.
- **Keeping Costs Low.** The more we produce, the less it costs. So we need to keep in mind and work with the manufacturers. I would imagine most manufacturers discuss the price and it in the contract. But there could be daily changes too.
- **Delivery.** We need to make sure our parts/products are delivered to the right places (manufacturers to manufacturers, manufacturers to retail, retail to retail).
- **Debug and Test.** We might need to fly our engineers to specific manufacturers to debug and/or test.
- **Supplying.** We would need to know how many products we need to supply to retailers in different regions. Some regions might have a sale and some might not, causing a shift in demands. We might also need to ship parts for repairs, unless everything is shipped to somewhere for repair, which doesn't seem so. Apple Stores can always do light repairs and have their own spare parts lying around for the easy fixes.

# Amazon Robot Picker

An Amazon Robot Picker requires a special fastener produced by a Japanese company. The end-to-end production of the special fastener comprises five different stations summarized below.

Which station is the bottleneck in the process? And what is the capacity of the assembly line, units per hour?

- Station 1: 45 seconds of processing time
- Station 2: 30 seconds of processing time
- Station 3: 55 seconds of processing time
- Station 4: 80 seconds of processing time
- Station 5: 20 seconds of processing time

# Answer

Station capacity:

- Station 1: 60/45 = 1.33 units per minute
- Station 2: 60/30 = 2 units per minute
- Station 3: 60/55 = 1.1 units per minute
- Station 4: 60/80 = 0.75 units per minute
- Station 5: 60/20 = 3 units per minute

Station 4 is the bottleneck.

The capacity of the assembly line is equivalent to the bottleneck, so the assembly line's capacity is 0.75 units per minute.

# Amazon Pick-and-Pack Utilization

Amazon’s pick-and-pack operation has the following processes:

- Pick station: 7 orders per 10 minutes
- Pack station: 11 orders per 10 minutes

What is the utilization of the pack station?

# Answer

Flow rate = 5 orders per minute

Utilization = Flow rate / Pack station capacity = 7 orders per 10 minutes / 11 orders per 10 minutes = 0.64

# Amazon Order Wait Times

During the holiday season, Amazon customers shipped 200 orders per second.

Amazon's data science team discovered that the average number of orders waiting to be shipped was 20,650.

How long did the average Amazon order wait to be shipped?

# Answer

Inventory = Flow rate * Flow time

20,650 orders = 200 orders per second * W seconds

Wait time is 103.25 seconds

# Inbound Flow

You are in charge of the department that receives the product into the building and stows it to the bin it is accessible by the department. You have two options on how to receive and stow the product. In the first option, you receive the product at 250 units per labor hour and stow it at 100 units per labor hour. You must receive it and stow it for the unit to count for production. This process results in 1% of the units stowed being incorrect. You can find and fix these errors at a rate of 20 units per labor hour with what you believe is almost 100% accuracy. In the second option, you receive and stow the product in one step vs. two. The rate for this process is 80 units per labor hours for receive and stow. This process results in 1.5% of the units stowed being incorrect. You can find and fix these errors at a rate of 20 units per labor hour with what you believe is almost 100% accuracy.

- Which option would you select for today's units and why?
- Does your answer change if you are told you must fully process 100,000 units today? If, why?
- Does your answer change if you are told that you have 15 associates today and you must fully produce the maximum units possible? If yes, why?

### Things to Consider

- Are all the associates-trained to both receive and stow?
- Aside from processing time, is cost an issue?
- Is it possible to do the two steps in parallel for option 1?

# Answer

CANDIDATE: Let's break these numbers down:

### Method 1

It takes 1 hour to receive 250 units, 2.5 hours to stow away these units at 100 units per hour. This takes 3.5 hours to process 250 units.

### Method 2

It takes 3.125 hours to receive and stow 250 units at 80 units per hour (250 / 80 = 3.125).

However, Method 2 results in 1.5% errors compared to 1% in Method 1.

Method 1: 3.5 hours + (2.5 hours * 0.01 / 20) = 3.5 + 0.125 = 3.625 hours.
Method 2: 3.125 hours + (3.125 hours * 0.015 / 20) = 3.125 + 0.234 = 3.359 hours.

Method 2 is faster.

If we need to process 100,000 units:
Method 1: (100,000 / 250) * 3.5 = 1,400 hours.
Method 2: (100,000 / 80) * 3.125 = 3,906.25 hours.

Method 1 is better.

If we have 15 associates:
Method 1 capacity: 250 * 15 = 3,750 units/hour.
Method 2 capacity: 80 * 15 = 1,200 units/hour.

Method 1 is better.

# Last Minute Supplier Problem

Something breaks in the project at the last minute and it is from a supplier. How will you solve it?

### Things to Consider

- What broke, and how important is it?
- How long will it take to fix?
- What are some alternatives to the broken part? How long will that take?
- What are the tradeoffs for the different options?

# Answer

CANDIDATE: This is a real broad question. Are we talking about a physical product?

INTERVIEWER: Yes.

CANDIDATE: Okay, then we are really facing with a certain part cannot be used, which halts our entire pipeline since losing a part means the product is not going to work. We are basically bottlenecked. I could see several problems:

- Technical or mechanical problem with our own parts. In other words, a faulty design.
- Supplier problems, such as labor unrest, geopolitical instability or some other factory downtime.
- The supplier suddenly wants a higher price. Since we should have a contract, this is unlikely, but it could happen.
- Too many parts produced.
- Too few parts produced.

INTERVIEWER: Out of all the problems, which one do you think happens most?

CANDIDATE: Technical problems followed by mechanical problems.

INTERVIEWER: So how would you address these issues?

CANDIDATE: To address each of these problems, here are some things I would consider:

- Send out an engineer. If it's a technical or mechanical problem with our own parts we can send out an engineer to help fix it.
- Alternative supplier. If the problem is with the suppliers, we can look for alternatives. We don't want to be bottlenecked on this part and cause a delay.
