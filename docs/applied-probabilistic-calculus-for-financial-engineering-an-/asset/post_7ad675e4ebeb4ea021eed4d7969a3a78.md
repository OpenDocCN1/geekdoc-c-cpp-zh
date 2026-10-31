
the gradients are zeros), *it is implicitly assumed that these minima do exist!* However, in probabilistic calculus, such minima, or even such turning points, may not exist or may not be readily located. Heuristic approaches may be called upon to locate any existing and available minima.

Some useful heuristic methodology in locating minima, and the corresponding R programs for minimization are discussed in the following sections.

### 6.2.1 The Evolutionary Algorithms (EA)

Optimization algorithms inspired by the process of natural selection have been in use since the 1950s, and are often referred to as evolutionary algorithms. The genetic algorithm is one such method, and was invented by Holland in the 1960s. Genetic algorithms apply logical operations, usually on bit strings of fixed or variable lengths, in order to perform crossover, mutation, and selection on a population. Following successive generations, the members of the population are more likely to be a minimum of an objective function. Genetic algorithms have shown to be useful heuristic methods for global optimization, in particular for combinatorial optimization problems. Evolution strategies are another variety of evolutionary algorithm. Genetic algorithms apply logical operations, usually on bit strings of fixed or variable length, in order to perform crossover, mutation, and selection on a population. Following successive generations, the members of the population are more likely to represent a minimum of an objective function.

Genetic algorithms are useful heuristic methods for global optimization, in particular for combinatorial optimization problems.

### 6.2.2 The Differential Evolution (DE) Algorithm

Another useful approach in portfolio optimization, particularly in assessing the equal risk contributions to the portfolio, is the differential evolution (DE) algorithm, introduced by Storn and Ulrich (1997), with its application demonstrated by Price, et al. (2006). It is considered to be a genetic algorithm, and is a derivative-free global optimizer.

The `DEoptim` implementation of DE was motivated by the objective of extending the set of algorithms available for global optimization in the R language and environment for statistical computing (R Development Core Team 2009). R enables rapid prototyping of objective functions, access to a wide array of tools for statistical modeling, and ability to generate customized plots of results with ease (which in many situations makes use of R preferable over the use of programs in languages like Java, MS Visual C++, Fortran 90, or Pascal). `DEoptim` is available at http://CRAN.R-project.org/package=DEoptim.

## 6.3 Financial Risk Modeling and Portfolio Optimization

In the real world of financial engineering, most private investors work through one or more “financial advisors”, which, in turn, work with “wealth management corporations.”

The following is an example of a typical financial advisor (Crystal Cove Advisors of Newport Beach, California), which invests via large professional organizations (such as the LPL Financial of San Diego, California).

### 6.3.1 An Example of a Typical Professional Organization in Wealth Management

### 6.3.1.1 LPL (Linsco Private Ledger) Financial

From Wikipedia (Figure 6.3):

*LPL Financial is one of the largest organizations of independent financial advisors in the United States of America. Formed in 1989 through the*

| Item | Details |
|---|---|
| LPL Financial | |
| Type | Public |
| Traded as | NASDAQ: LPLA |
| Industry | Financial services |
| Founded | 1968 |
| Headquarters | 75 State Street<br>Boston, Massachusetts |
| Key people | Mark Casady, Chairman & CEO |
| Revenue | ▲ US$4.37 billion (2014) |
| Number of employees | 3,384 |
| Parent | LPL Financial Holdings Inc. |
| Website | www.lpl.com |

Figure 6.3 LPL Financial.

merger of two brokerage companies – **Linsco** (established in 1968) and **Private Ledger** (established in 1973) – LPL has since expanded its number of independent financial advisors to more than 14,000. LPL Financial has main offices in
- Boston, MA,
- Charlotte, NC, and
- San Diego, CA

covering the eastern, southern, and western regions of the United States, respectively, as well as other associated territories.

Approximately 3500 employees support financial advisors, financial institutions, and technology, custody, and clearing service subscribers with enabling technology, comprehensive clearing, and compliance services, practice management programs and training, and independent research.

LPL Financial advisors support clients with a number of financial services, including equities, bonds, mutual funds, annuities, insurance, and fee-based programs. However, LPL Financial does **not** develop its own investment products, thus enabling the firm’s investment professionals to offer financial services ostensibly free from broker/dealer-inspired conflicts of interest.

Additional information on LPL
- 1) Recent Timeline
- 2) Some Important Statistics
- 3) External links

### 6.3.1.1.1 Recent Timeline

In 1989, LPL Financial was created through the merger of two small brokerage firms *Linsco* and *Private Ledger*.

In 2003, LPL Financial acquired Private Trust Company, which manages trusts and family assets for high-net-worth clients in all 50 states.

In 2004, LPL Financial acquired the broker/dealer operations of the Phoenix Companies, which offered Phoenix the chance to sell its products through the LPL Financial network.

In 2005, private equity firms Hellman & Friedman and Texas Pacific Group took a 60% stake in the firm.

In August 2006, LPL Financial expanded its client base following the purchase of UVEST Financial Services, which provided independent brokerage services to more than 300 regional and community banks and credit unions throughout the United States.

In June 2007, LPL Financial finalized its acquisition of several broker/dealers under the Pacific Select Group (aka Pacific Life) umbrella, which added 2000 financial advisors.

In September 2007, LPL Financial and Sun Life Financial announced a definitive agreement under which an affiliate of LPL Financial acquired Independent Financial Marketing Group, Inc. (IFMG) from Sun Life Financial. Sun Life Financial is a leading international financial services organization. The LPL Financial Institution Services business unit, which manages the IFMG business, is the nation’s top provider of investment and insurance services to banks and credit unions. The deal closed in November 2007.

On January 1, 2008, Linsco/Private Ledger Corp. (LPL Financial Services) changed its brand name to “LPL Financial.”

On November 18, 2010, LPL Investment Holdings Inc., the parent company of LPL Financial, became a publicly traded company on the NASDAQ Stock Market under ticker symbol LPLA.

In 2011, LPL Financial acquired New Jersey-based Concord Capital Partners, which helps trust companies automate the business practices of their internal investment management activities.

In January 2012, LPL Financial acquired Rockville-based Fortigent, which provides high-net-worth solutions and consulting services to RIAs, banks, and trust companies.

In November 2015, LPL Financial announced its first advisor online tool suite certification for Investment Support Services.

### 6.3.1.1.2 Some Important Statistics

Key facts regarding LPL Financial include the following:
- 4.5 million funded accounts
- 14,000 *financial advisors* supported
- Approximately 4500 technology, custody, and clearing service subscribers
- Approximately 700 financial institution partners
- $475 billion in advisory and brokerage assets

### 6.3.1.1.3 External links

- LPL Financial Web site
- LPL Financial recruiting Web site

As an example of a typical independent “Financial Advisor” serving the public (for a fee), through LPL, consider the following

### Crystal Cove Advisors

- Crystal Cove Advisors is an investment management firm located in Newport Beach, California. Its team of professionals will provide clients with investment strategies that focus on *limiting risk while seeking profitable results*. It believes that avoiding serious loss is the best way to increase long-term returns.
