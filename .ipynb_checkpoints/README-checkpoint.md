# RoboAdvisor - The Power of the Cloud 

### Robo Advisor for Retirement Plans

![Robot](Images/robot.jpg)

*Photo by [Alex Knight](https://www.pexels.com/@alex-knight-1272316?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/high-angle-photo-of-robot-2599244/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) | [Free License](https://www.pexels.com/photo-license/)*

### Background

Digital transformation consultant, hired by most prominent retirment plan providers in the country would like to increase their client portfolio, especially by engaging young people. Since machine learning and NLP are disrupting finance to improve customer experience, robo advisor is created that could be used by customers or potential new customers to get investment portfolio recommendations for retirement.

### Packages Used:

* Amazon Lex [Amazon Lex Bot](https://aws.amazon.com/lex/)
* Lambda [Amazon Lambda](https://aws.amazon.com/lambda/)

### Files

* [lambda_function.py](Starter_Files/lambda_function.py)
* [correct_dialog.txt](Test_Cases/correct_dialog.txt)
* [age_error.txt](Test_Cases/age_error.txt)
* [incorrect_amount_error.txt](Test_Cases/incorrect_amount_error.txt)
* [negative_age_error.txt](Test_Cases/negative_age_error.txt)

---

#### Tasks Performed:

<details>
<summary>1. **[Initial Robo Advisor Configuration:](#Initial-Robo-Advisor-Configuration)** </summary>

> Define an Amazon Lex Bot with a single intent that establishes a conversation about the requirements to suggest an investment portfolio for retirement.

> Sign in into AWS Management Console and create a new custom Amazon Lex bot `RoboAdvisor`. 

> Setup the following parameters:
    > * **Bot name:** RoboAdvisor
    > * **Output voice**: Salli
    > * **Session timeout:** 5 minutes
    > * **Sentiment analysis:** No
    > * **COPPA**: No

> Create the `RecommendPortfolio` intent, and configure some sample utterances as follows: 
    > * I want to save money for my retirement
    > * I'm ​`{age}​` and I would like to invest for my retirement
    > * I'm `​{age}​` and I want to invest for my retirement
    > * I want the best option to invest for my retirement
    > * I'm worried about my retirement
    > * I want to invest for my retirement
    > * I would like to invest for my retirement

<img src="Images/sample_utterances.PNG" width="500" />  

> Slots used by the bot, three using built-in types and one custom slot named `riskLevel`. The three initial slots as follows:

| Name             | Slot Type            | Prompt                                                                    |
| ---------------- | -------------------- | ------------------------------------------------------------------------- |
| firstName        | AMAZON.US_FIRST_NAME | Thank you for trusting on me to help, could you please give me your name? |
| age              | AMAZON.NUMBER        | How old are you?                                                          |
| investmentAmount | AMAZON.NUMBER        | How much do you want to invest?                                           |

  > The `riskLevel` custom slot will be used to retrieve the risk level the user is willing to take on the investment portfolio; create this custom slot as follows:

   > * **Name:** riskLevel
   > * **Prompt:** What level of investment risk would you like to take?
   > * **Maximum number of retries:** 2
   > * **Prompt response cards:** 4

<img src="Images/slots.PNG" width="500" />

> Configure the response cards for the `riskLevel` slot as is shown bellow:

| Card 1                              | Card 2                              |
| ----------------------------------- | ----------------------------------- |
| <img src="Images/card1.PNG" width="400" />  | <img src="Images/card2.PNG" width="400" />  |

| Card 3                              | Card 4                              |
| ----------------------------------- | ----------------------------------- |
| <img src="Images/card3.PNG" width="400" />  | <img src="Images/card4.PNG" width="400" />  |


> Move to the *Confirmation Prompt* section, and set the following messages:
    > * **Confirm:** Thanks, now I will look for the best investment portfolio for you.
    > * **Cancel:** I will be pleased to assist you in the future.

> Leave the error handling configuration for the `RecommendPortfolio` bot with the default values.

<img src="Images/error_handling.png" width="500" />

</details>


<details>
<summary>2. **[Build and Test the Robo Advisor](#Build-and-Test-the-Robo-Advisor):**</summary>

> Build the bot and test it in the chatbot window to ensure accurate user conversation.

![Robo Advisor test](Images/bot-test-no-lambda.gif)

</details>

<details>
<summary> 3. **Enhance the Robo Advisor with an Amazon Lambda Function:** </summary>

> Create an Amazon Lambda function `recommend_portfolio()` to validate the data provided by the user on the RoboAdvisor.

> Starter code provided on [lambda_function.py](Starter_Files/lambda_function.py)
    
> User input Validation guidelines to complete `recommend_portfolio()`
    > * The `age` should be greater than 21 and less than 65.
    > * the `investment_amount` should be equal to or greater than 5000.

> Investment Portfolio Recommendation based on the selected risk level criteria, response from the bot should be as: 
        > * **none:** "100% bonds (AGG), 0% equities (SPY)"
        > * **very low:** "80% bonds (AGG), 20% equities (SPY)"
        > * **low:** "60% bonds (AGG), 40% equities (SPY)"
        > * **medium:** "40% bonds (AGG), 60% equities (SPY)"
        > * **high:** "20% bonds (AGG), 80% equities (SPY)"
        > * **very high:** "0% bonds (AGG), 100% equities (SPY)"

> Test the Lambda function using the [sample test cases](Test_Cases/) provided.

> Open the Amazon Lex Console and navigate to the `RecommendPortfolio` bot configuration, integrate the lambda function `recommend_portfolio()` by selecting it in the _Lambda initialization and validation_ and _Fulfillment_ sections.

![bot-test-with-lambda](Images/bot-test-with-lambda.gif)

---
