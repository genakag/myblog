## Leading zeros in CSV data

Exporting to CSV is not always a fun task but it is usually required because it makes it easier for other people to analyze the data. I recently implemented a feature to export data to CSV but some people had trouble using the data. The software people were using, like Microsoft Excel and Google Spread Sheets, modified the data after opening the CSV file. Although the actual CSV data was correct, it was very hard to prevent Excel and similar software to remove the leading zeros so I ended up fixing the code.

## The problem I had
The leading zeros for numbers were deleted when the CSV file was opened with Excel. This may be okay for most of the use cases, but for some, it was problematic. This was a problem for my use case because I was representing phone numbers and zip codes with just numbers.

### Example

CSV data

|phone number|zip code|
|-|-|
|08012345678|0070011|

When opened in Excel

|phone number|zip code|
|-|-|
|8012345678|70011|

As you can see in the example above, the leading zeros were removed when the CSV file was opened in Excel. It was not a problem of formatting, but the zeros were actually removed. Both Excel and Spread Sheet removed the leading zeros.

### How I solved it
I solved it by making Excel recognize the data as a String type instead of a Number type. I simply put dashes between some of the numbers so that it was in the format that people usually write phone numbers. I did something similar with the zip code too.

|phone number|zip code|
|-|-|
|080-1234-5678|007-0011|

I think adding a non-number symbol somewhere in the number makes Excel recognize the data as a String. This also worked with Spread Sheets.

## Conclusion
When creating CSV data, you should prevent having String type data with just numbers. Data with just numbers are going to be recognized as a Number type and the leading zeros will be truncated. Adding some symbols somewhere in the String will prevent this.

## Thanks!
Thank you for reading till the end. I hope you find this useful!
