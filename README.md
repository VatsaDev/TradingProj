# stocks GC

`general warning, I'm better at the ML side, not the finance side. if anyone has an idea/strat for the financial side (ex. options/futures/etc, any non-stock), try it`

`btw, how profitable your strat is/how fast it grows money is called sharpe. DO NOT prioritize this over everything else, because Sharpe doesnt scale. a sharpe of 5 on $1000 is nothing next to a sharpe of 2 on $10000`

## General resources

 - book on forecasting, most likely helpful: https://otexts.com/fpp2/intro.html
 - [entire WIKI on Algo Trades](https://www.reddit.com/r/algotrading/wiki/index/)
 
This is a general principles link: https://www.hudsonrivertrading.com/hrtbeat/trading-machine-learning/
we need to follow these to actually document all our work with each strat, then we can review them all and find a most optimal strat

TLDR btw:

 - document everything, make loss graphs, plot model results, document your process, everything, we need it all to actually verify and reproduce any results you have and to know the pros and cons of all our actions
 - be simple/robust, dont try anything fancy unless it has some form of direct substantial benefit, and try to be consistent with what you do
 - we dont really care about generalizing that much, its not nesc, because we are focused on our specific finance domains for each strat, but if you do think something might work for one of the other strats, let the person working on it know

## possible strats 

 - strat 1: industry defaults (LSTMs)
 - strat 2: Dr. Agah paper (the paper)
 - strat 3: time-series models
 - Strat 4: ML for Arbitrage
 - Strat 5: emulate day trade signals
 - Strat 6: ML for HFT (high frequency trading)

## Industry defaults

 - build an LSTM
 - probably our least innovative, but has many tutorials and stuff avalible

links (tried to rate from easiest to hardest):

 - https://www.reddit.com/r/algotrading/comments/123bgnv/working_example_of_an_lstm_model_for_predicting/
 - https://www.reddit.com/r/learnmachinelearning/comments/ej48yi/problem_with_lstm_stock_price_prediction/
 - https://www.reddit.com/r/algotrading/comments/mxijbd/using_an_lstm_for_stock_price_prediction/
 - https://www.linkedin.com/pulse/how-machine-learning-used-predicting-stock-prices-lstm-vignesh-n/
 - https://medium.com/@prajjwalchauhan94017/stock-prediction-and-forecasting-using-lstm-long-short-term-memory-9ff56625de73
 - https://www.nature.com/articles/s41599-023-02042-w
 - https://cs230.stanford.edu/projects_winter_2020/reports/32066186.pdf

## Dr. Agah Paper 

 - paper for reference: https://www.degruyter.com/document/doi/10.1515/jisys-2017-0567/html

 - Bascially it has two parts, the *Text analysis* and *Time series*

 - data collection
     - Our main sources will probably be finance social media, reddit/twitter+cnn+google trends+yahoo finance+reports by companies/firms, maybe weight them by follower count/upvotes (probably a direct correlation for influence and stock price for that)
     - increase scrape parameters to more topics (commodities, oil/gas/diamonds/etc, nyse/nasdaq words, etc), then process it, much more than the $stocks

 - Text stuff 
     - He tried to build linear classifiers and svms and stuff for text, we can massively simplify that part by just giving the text to the gemini api and asking for details 
     - [gemini api tutorial](https://aistudio.google.com/)

     - possible questions/ideas to try on the text front:
         - target specific stocks/parts of statements for extraction
         - input several texts from a small span of time and ask for a long/short or buy/sell signal
         - the paper mentions the effects of pre-news (ex. twitters users having information before CNN publishes it), figure out ways to use this
         - how much do the movements of large groups/quant funds/research teams matter? ex. negative citadel/Jane st. tweet=small short, or another hindenburg research tweet=short stock, even if its just one datapoint?
       - also find out if its better to short or long more often in this strat

 - time series 
     - just another LSTM that used the text signals for buy/sells

## Time series models

This is bascially strat 1 but trying it out with modern timeseries models to see if they are better than LSTMs somehow

Papers for reference:

 - Google deepminds time series model: https://research.google/blog/a-decoder-only-foundation-model-for-time-series-forecasting/
 - Amazon researchs time series model:
     - https://arxiv.org/pdf/2403.07815v1 (paper)
     - https://github.com/amazon-science/chronos-forecasting (code, but you probably need to reprogram it all yourself for the stock adaptation)

## Model Arbitrage

 - ML models, but for financial arbitrage, probably the next best tutorial based one, lots of stuff for it out there

Links to possible methods:

 - https://github.com/ericcccsliu/imc-prosperity-2/tree/main?tab=readme-ov-file `literal competition wins with strats and examples`
 - https://theaiquant.medium.com/statistical-arbitrage-and-pairs-trading-with-machine-learning-875a221c046c
 - https://www.mathworks.com/help/finance/machine-learning-for-statistical-arbitrage-introduction.html
 - https://www.mathworks.com/help/finance/machine-learning-for-statistical-arbitrage-ii-feature-engineering-model-development.html
 - https://cfe.columbia.edu/sites/default/files/content/slides/MarkusPelger_Slides%20Deep%20Learning%20Statistical%20Arbitrage.pdf `Literal powerpoint with examples`
 - https://www.vertoxquant.com/p/trading-on-prediction-markets
 - https://www.vertoxquant.com/p/sports-betting-arbitrage-how-anyone
 - https://www.algos.org/p/event-based-alpha-a-quick-guide?utm_source=profile&utm_medium=reader2
 - https://www.algos.org/p/breaking-down-momentum-strategies?utm_source=profile&utm_medium=reader2
 - https://cs229.stanford.edu/proj2019spr/report/26.pdf
 - https://www.sciencedirect.com/science/article/pii/S1877050922005610

Other intresting/maybe useful links:

 - https://substack.com/@quantarb/p-101268706
 - https://www.algos.org/p/deploying-strategies-helpful-advice?utm_source=profile&utm_medium=reader2
 - https://www.algos.org/p/where-will-crypto-go?utm_source=profile&utm_medium=reader2
 - https://www.algos.org/p/options-volatility-quant-resources?utm_source=profile&utm_medium=reader2
 - https://www.algos.org/p/outliers-a-deep-dive-part-1?utm_source=profile&utm_medium=reader2
 - https://www.algos.org/p/timeframe-crowding-an-interesting?utm_source=profile&utm_medium=reader2
 - https://www.algos.org/p/alpha-pipeline-raw-data-trades?utm_source=profile&utm_medium=reader2
 - https://www.algos.org/p/election-cycle-seasonality-effects?utm_source=profile&utm_medium=reader2 `important, we are in an election year, possibly useful`

## Emulate Day Trade signals 

 - ML algos that mimic day traders, attempt to make the models learn profitable strats for small amounts, then try to scale this horizontally with more traders and more accounts rather than vertically with money 

resources:
 - https://www.youtube.com/watch?v=iBNcF_lPBIg&list=PL1xI23WKVWifWxQG4aNCa-bo_RyIrqEyR (growing money from $1k to $1M series)
 - https://www.youtube.com/watch?v=QstdS67Iyv0&list=PL1xI23WKVWifg6nqTu2sMZVF8nWfQ8udX (default stuff we should try to emulate in the model)

## High frequency trading ML 

 - Needs research, but basic ideas revolve around algos working fast enough to simulate a stock for a period of time and then let something else make the trade, or just be a fast algo and let the ML do stuff 

Research to Explore:

 - https://www.linkedin.com/pulse/high-frequency-trading-machine-learning-algorithms/ 
 - https://souravsengupta.com/cds2015/lectures/DMukherjee_Notes.pdf
 - https://arxiv.org/abs/2405.08101
 - https://www.cis.upenn.edu/~mkearns/papers/KearnsNevmyvakaHFTRiskBooks.pdf
 - https://github.com/bradleyboyuyang/ML-HFT
