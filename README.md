# MeanReversionNeuralNetowrkForStockPrediction

     ・"Mean Reversion" on stock price.
     ・Fucuses on Data Processing before & after the machine learning
     ・The Neural Network structure itself is very simple.

"Mean Reversion", or Moving Average Analysis is the most popular way of predicting stock prices. Things retruns to its average. 

Using the simple structure of the Neural Network (NN), the divergence rates sequence from moving average curve gives a prediction of up/down direction about stock price. This project is tested by Nikkei225 index. The NN structure modeled by tensorfllow is simple and audinally one. As is usual, data pre-processing or preparation play the most important part on machine learning.
This repo focuses on showing an example of processing input data from row stock price and of an interpretation about the output.

Also explains about predicting by the Simple NN.
Additionally, shows some applications to develop an iOS App through the AWS cloud.

■ Contents ■

      1. Data Proccesing
      2. Emphasize meaning of inputs and Machine Learning
      3. Prediction and output interpretation

■ 1. Data Proccesing ■

  First, we develop the input data. The file "ratio.py" generates the input for the NN.
  Raw data example is in the repo named "ex_N225_index.csv". This project has tested by Nikkei225 index's close price, but another stock prices or indices can be applied for.

  (Command)
  
      A. Move the foloder (using -cd command etc.) including ratio.py and row data. 
      B. Run by -python command. (On terminal, "-python ratio.py")

  (Explanation)
  
   Algo in "ratio.py" finds maximum poles and minimum poles on the moving average (curve). From them, it decides "peaks and bottoms" of the price during the terms. Then, it generates accelarations (UP_RATIOs) from each peak and bottom. The accelaration means the speeds of differences from the peaks and bottoms. The input data for the NN consits of 25 days' differences of stock prices from moving average and the accelaration at the day, as the example (ex_input.csv) shows.
   
  (! Disclaimer)
  
   The output(the input for NN) possibly includes exceptions. Because of the "peaks and bottoms" are difined by artificiallly, mechanically, or judged by the algolism bellow shows for proccesing such a big data in a short time, cases are that, there possibly includes some exceptions, which doesn't seems to be the peaks or bottoms in the term.

■ 2. Emphasize the meaning of inputs and Machine Learning ■

   Translation of both input and output data is essencial for the simple NN. 
 
 (★ Emphasize ★)
 
    Before running this code, you need to adjust of the input data to "Emphasize" the meaning of the time series.
    "UP_RATIO (Accelaration)" is, to be adjusted in the 3 steps bellow.
    
      Step 1.
      Adopt the accelaration which gives the maximum absolete during past 5 days.
    
      Step 2.
      On Step 1. accelaratons, adopt the one gives the maximum absolete during 5 days, from 2 days before to 2 days past, including the day.
    
      Step3.
      Normalize the accelarations by its maximum and minimum during all the term.
    
   The NN uses "the adjusted accelarations" together with 25 differencials as a input.
   Please renew the "input.csv" by "adjudted" UP_RATIO (accelaration).
   -> A line consists of 25 differencials and "adjusted" accelaration.
   (Named the input as "input.csv".)

 (Why need the adjustments?)
 
   The row accelaration data has large variation or deviation, so the NN can't read the meaning of the time series. Before training, emphasize the trend and make it easy to understand for the NN.
 
 (Machine Learning)
 
   Trained by the 80% of the input data as the teacher data (rest of the 20% are for the test), the simple NN gives a prediction of stock direction (acceralation) inputted by 25 days' differences of current prices.
  
  (NN Structure)
  
     ・Input layer(25 nodes) -- Medium layer (25) -- Output layer (1)
     ・Active function of the Medium is sigmoid, that of the Output is tanh
     ・Loss function is squared error
   
  (★★ Tuning and adjustment of ERROR_RANGE ★★)
  
  Set the ERROR_RANGE judging the correct answer or not for yourself.
  ! This is up to the users and set the ERROR_RANGE one by one with try and error based on the interpretation of the prediction as the way section 3 shows.
   
   (Command)
   
  After adjusting accelaration (:Step 1~3) and setting of the error range, enter the command:
 
      A. -cd to the folder including nn_stock.py, input.csv
      B. -python nn_stock.py
      Adjust the ERROR_RANGE with try and error, based on the interpretation of prediction as the way section 3 shows.

  The outcome "model", "model.meta", "checkpoint" are the trained NN model.
  
■ 3. Prediction and output interpretation ■

    Load the model and predict the accelaration by the real stock prices.
    Prepare the market data in real. The input needs 25 close stock prices (index prices). 25 differencials form the moving average will be generated by the code. The model uses 25 differencials as input and produce 1 prediction data (accelaration). The accelaration is the direction of the stock price.
  
   (Command)

     A. -cd to the folder including "nn_stock.py", "N225_index.csv", and traind model: "model", "model.meta", "checkpoint".
     B. -python nn_stock.py
     
   (★★★ Interpretation of the predictions ★★★)
   
   The predicted accelarations has large variation or deviation, similar to the input data, so you need to get moving average of the prediction time series to get smoother the outputs. Getting average or leveling predictions is like interpretation or translation of machine language to human's to understand the deviation or angiguity of the outcomes generated by AI.
    
■ As you read, the data emphasis and data leveling are more important than to create more complicated neural network models. ■


