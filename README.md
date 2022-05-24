# Analysis of Green Company Stocks

## Based on trends in the data, what is the best stock to invest in for a green company

### The purpose of this analysis is to see what trends are present in green energy company stocks, and the current investment company DAQ. These outcomes will help decide the best investment to make for stock trading in green energy.

## Analysis and Results

#### For this analysis I have created the ability to run a stocks analysis to find the stock’s volumes and returns of our green energy company stocks. This allows us to see trends and outcomes so that finial decisions can be made for the best financial investment opportunities. 

### Using Macros in Excel’s VBA developer tools.

#### Through Excel’s VBA developer tool, we can automate the process of data analysis for the green energy company stocks data we have collected based on the years 2017 and 2018 by creating a Macro, or Subroutine, of code. 
  Using the VBA code [Sub AllStocksAnalysis()] I created a subroutine which will pull the returns for green energy company stocks for the inputted year and the total daily volume. Within this routine I have first used the code [Dim startTime as Single, Dim endTime as Single] to create data types for the macro to evaluate how long it takes for the code to run. Then using the code [yearValue = InputBox("What year would you like to run the analysis on?") startTime = Timer], a input box will pop up allowing the user to enter the year they would like stock analysis on. This code will also tell the macro to begin the timer for the code runtime. Next I will start with the code [Worksheets("All Stocks Analysis").Activate] to activate which worksheet the macro will be running on. From there I then use [Range("A1").Value = "All Stocks(“ + yearValue +”] to set the value of cell A1 to “All Stocks (year inputted by user)”. I create a header row using [Cells(3, 1).Value = "Year", Cells(3, 2).Value = "Total Daily Volume", Cells(3, 3).Value = "Return"] to set the value of the cells to our header text. The next part of the code initializes an array, or list, of all the stock tickers. This action uses the following code [Dim tickers(12) As String, tickers(0) = "AY", tickers(1) = "CSIQ", tickers(2) = "DQ", tickers(3) = "ENPH", tickers(4) = "FSLR", tickers(5) = "HASI", tickers(6) = "JKS",  tickers(7) = "RUN",  tickers(8) = "SEDG", tickers(9) = "SPWR", tickers(10) = "TERP", tickers(11) = "VSLR"]

  To activate which worksheet I want to pull the requested information from I use the code [Sheets("yearValue").Activate] then I get the number of rows for the code to loop over using [RowCount = Cells(Rows.Count, "A").End(xlUp).Row]. I create a ticker Index using the code [tickerIndex = 0]. Now I create three output arrays for our data using code [Dim tickerVolumes(12) As LongLong, tickerstartingPrices(12) As Single, Dim tickerendingPrices(12) As Single].  I created code to loop to intitialize the tickerVolumes to zero using the code loop [For I = 0 To 11, tickerVolumes(i) = 0, Next i]. To loop over all of the rows contained in the spreadsheet I used the following code [For i = 2 To RowCount]. Next I use the code [tickerVolumes(tickerIndex) = tickerVolumes(tickerIndex) + Cells(i, 8).Value]  to increase the current ticker’s volume, To check if the current row is the first withing the selected tickerIndex I use and “If Then” code [If Cells(i - 1, 1).Value <> tickers(tickerIndex) Then, tickerstartingPrices(tickerIndex) = Cells(i, 6).Value,  End If].  To check if the current row is the last row withing the selected data and then correct it by increasing the tickerIndex by one if it doesn’t match, the code [ If Cells(i + 1, 1).Value <> tickers(tickerIndex) Then, tickerendingPrices(tickerIndex) = Cells(i, 6).Value, tickerIndex = tickerIndex + 1, End If] is applied.
  
  Now the data gets output onto the worksheet “All Stocks Analysis” so that it can be viewed. To do this I used the code [Next I, For i = 0 To 11, Sheets("All Stocks Analysis").Activate, Cells(4 + i, 1).Value = tickers(i), Cells(4 + i, 2).Value = tickerVolumes(i),  Cells(4 + i, 3).Value = tickerendingPrices(i) / tickerstartingPrices(i) - 1]. The final part of the code for this macro is the formatting code. This allows the worksheet text and cells to have specific font styles and colors applied to them all from withing the macro versus application by the user. First is the activation of the worksheet for the formatting to be applied to using [Sheets(“All Stocks Analysis”).Activate]. From there I state which fonts and style to apply to which rows using the following code [Range("A3:C3").Font.FontStyle = "Bold", Range("A3:C3").Borders(xlEdgeBottom).LineStyle = xlContinuous, Range("B4:B15").NumberFormat = "$#,##0", Range("C4:C15").NumberFormat = "0.0%", Columns("B").AutoFit]. The last part of the formatting code applies color settings to the cell based on the value of the data within the cell. This lets the user see at a quick glance what stock returned positively or negatively using green and red color formatting with the “If, Then” code [dataRowStart = 4, dataRowEnd = 15, For i = dataRowStart To dataRowEnd, If Cells(i, 3) > 0 Then,  Cells(i, 3).Interior.Color = vbGreen, Else Cells(i, 3).Interior.Color = vbRed, End If,  Next i]. To close the timer that was initiated at the beginning of this code and provide a pop-up box with the results I use the code [endTime = Timer, MsgBox "This code ran in " & (endTime - startTime) & " seconds for the year " & (yearValue)]. The last bit of code [End Sub] tells the macro that the sub routine is finished.

  Comparing the stock performance between 2017 and 2018 we can see that most of the green company stocks, apart from TERP, most of the stocks did well in 2017. In the following year of 2018, most of the stocks have a drop in return, except for two companies, ENPH and RUN. Looking at the data in 2017 it shows that ENPH had a Total Daily Return of $221,772,100 with a 129.5% Return. In 2018 while ENPH had a slight drop to 81.9% Return, but the Total Daily Volume still did exceptionally at $607,473,500.  The other green company stock that did will is RUN. In 2017 RUN had a Total Daily Volume of $267,681,300 and a Return of 5.5%. While this seems like a relatively low return if we look at 2018 it jumps up.  In 2018 RUN had an increase to 84.0% Return and a Total Daily Volume of $502,757,100.
When you compare the refactored code to the original code there is a difference in run times. The original run of the code, it ran 2017 in 0.6289063. In the new refactored code for 2017, there is a difference of 0.5117188 quicker, with the new run time at 0.1171875. The original run of the code, it ran 2018 in 0.5898438. In the new refactored code for 2018, there is a difference of 0.4804688 quicker, with the new run time at 0.109375.
![VBA_Challenge_2017 png](https://user-images.githubusercontent.com/103263248/170134443-bc2e63bf-6dc1-46f4-b917-379b5ec9cf63.png)
![VBA_Challenge_2018 png](https://user-images.githubusercontent.com/103263248/170134449-579dd8c4-315e-46b6-ada4-91e183382c15.png)



## Summary

### Avantages and disadvantages of refactoring code
  There can be many advantages of refactoring code. One of these is that it allows code to be easier to maintain, make less complex, which in turn allows it to be easier to be read by the creator and collaborators. This also helps make bugs easier to find and fix. 
There can also be disadvantages to refactoring code. Some of these include that it can be very time consuming to rename variables and move parts of code around. This can also lead to the introduction of new bugs and errors into the code, which can lead you to get stuck and have trouble figuring out how to continue refactoring.

### Pros and Cons of refactoring the original VBA script
  The advantages encountered by refactoring the code for this VBA are that I was able to reduce the amount of code by creating nested loops and managing to shorten the runtime of the macro. This also makes the code less complex and easier to read. The disadvantage to refactoring the code is that it was easier to introduce new bugs into the code when adding loops and “if, then” statement to it. Once a new error was unintentionally added it was hard to pinpoint how to fix it, which made the whole process a bit time consuming to do. 
