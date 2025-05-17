Problem Statement
Using Historical stock Price data given for a company can we predict the future stock price for future?

Review:
There are number of statistical models like Arima forecasting, Linear Regression, but none of them take place long term dependencies into consideration. In this regard, Deep learning techniques use be saviour as they are good in capturing long term dependencies.

"Hence standard RNNs fail to learn in the presence of time lags greater than 5 – 10 discrete time steps between relevant input events and target signals. The vanishing error problem casts doubt on whether standard RNNs can indeed exhibit significant practical advantages over time window-based feedforward networks. A recent model, “Long Short-Term Memory” (LSTM), is not affected by this problem. LSTM can learn to bridge minimal time lags in excess of 1000 discrete time steps by enforcing constant error flow through “constant error carrousels” (CECs) within special units, called cells" 𝙍𝙚𝙛𝙚𝙧 𝙩𝙤 𝙩𝙝𝙞𝙨 𝙥𝙖𝙥𝙚𝙧 : https://ieeexplore.ieee.org/document/9005997

— Felix A. Gers, et al., Learning to Forget: Continual Prediction with LSTM, 2000

Data Set:
The We used stock Price for about 12 years for dataset, we got out dataset from National Stock Exchange(NSE) for three companies: SBI, YesBank and HDFC Bank stock price. Daily High, Low, Open, Close values were taken collected from credible website. The dataset can be assessed from the dataset folder.

Data Preprocessing:
First of all We created a windowed dataset where each data point comprising of 5 time-steps at the gap of 1 day, so 5 days 1 data point, the stock price for next day is given as the output for that data point. Then we split dataset in training to validation/test ratio 80 % to 20 %.

Approach
Enough emphasis has been laid on using LSTM Layers. So, furthur we discuss what makes our approach different from others :



Training
During the training process, we simply fit each training input using 'Adam Optimizer' with default learning rate, 0.001 and loss function mse on 500 epochs

Testing
Let us define what is Feedback loop:

** Feedback loop:

** say you are on day 1 of the test data, you already have learned weights from the model fitting on training data. For prediction on test data we assume that we want is model to give more weight to what was the market condition in last 20 days. So we want to customise our model to learn this 20 days time window so we train our trained model again on the data window of last 20 days which consists of last 17 data points because last in training set data point already contains the data for last 5 days we need 16 days more, then after fit model on these 17 data points for 10 epoches we predict on last day, and repeat the same for future timesteps. This testing method ensures more weight to recent happenings in the market.
