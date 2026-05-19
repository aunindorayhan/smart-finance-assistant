# Developer's Diary

## Project: Smart Finance Assistant

This project was developed as a Smart Finance Assistant using Python and Google Colab. The goal was to create a practical finance tool that can clean transaction data, handle messy currency formatting, separate refunds from spending, calculate category summaries, compare spending against a weekly budget, and generate simple financial insights.

## Development Process

I followed a structured six-step development process. First, I defined the finance problem and identified the main user need: helping a non-technical user understand their spending from transaction data. I then planned the required inputs and outputs, including Date, Amount, Category, Description, weekly budget, cleaned transaction data, category summaries, refund totals, net spending, and financial recommendations.

After planning the inputs and outputs, I worked through manual examples to understand the expected calculations. This helped me check that positive amounts should be treated as spending, negative amounts should be treated as refunds, and net spending should be calculated after subtracting refunds from total positive spending.

## AI Collaboration

AI was used as a development partner throughout the project. I used AI to brainstorm the finance problem, review pseudocode, improve Python functions, identify useful test cases, and refine the documentation. I did not simply copy AI responses without checking them. I reviewed whether the suggestions matched the business problem, whether the code produced useful outputs, and whether the final assistant would be understandable for a non-technical user.

AI was especially useful when converting the pseudocode into Python functions. It helped structure the data cleaning function, spending analysis function, recommendation generator, RAG-style guidance section, savings calculator, and testing strategy.

## Debugging and Testing

During development, I encountered several issues. One issue was a `NameError`, where variables such as `df_sample` or libraries such as `pd` were used before the required setup cells had been run. I resolved this by running the notebook in the correct order and ensuring that pandas and the sample transaction dataset were created before running the analysis functions.

Another issue occurred when some advanced AI connection cells required an API key or external server connection. These were not essential for demonstrating the main finance assistant, so I focused on reliable local Python functions that could run successfully inside the notebook.

The assistant was tested using normal transaction data, refund transactions, messy currency formatting, missing data, invalid values, missing required columns, and weekly budget comparison. These tests helped confirm that the assistant can clean data, separate refunds, calculate summaries, identify high spending categories, compare spending against a budget, and produce clear financial insights.

## Final Reflection

This project helped me understand how AI-assisted development can support a business information systems task when used critically. The final Smart Finance Assistant demonstrates data processing, financial analysis, user-centred design, testing, debugging, documentation, and AI-assisted development skills.

The most important lesson was that AI suggestions still need to be reviewed, tested, and adapted. The final notebook is stronger because the code was checked with sample data, errors were debugged, and the outputs were written in a clear, business-friendly way.
