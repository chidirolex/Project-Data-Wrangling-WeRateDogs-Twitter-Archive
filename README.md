# Project-Data-Wrangling-Welovedogs-Twitter-Archive
In my journey to working with the #welovedog tweeter data. I will break this report into three just like from our class.
## Gather
In this stage, I was able to gather data from three different source.
First: The directly download of the WeRateDogs Twitter archive data (twitter_archive_enhanced.csv)
Second: Use the Requests library to download the tweet image prediction (image_predictions.tsv) from the url provided.
Lastly: Use the Tweepy library to query additional data via the Twitter API (tweet_json.txt)
## Assess
This stage was very insightful and important as messy and dirty data would ruin any analysis. One really needs a third eye to find the messy and dirty areas in the data. I assessed the data `visually and programmatically` and found some huge pile of dirt ready to be cleaned.
The issues found were divided into `Quality` and `Tidiness` issues. In the next phases which involves cleaning we shall discuss how each issue and how they were cleaned.

Cleaning Stage
### Quality
After making a copy of the initial datasets, we start with our issues.
### Issue #1: Drop some features that are not needed (Most had lots of missing values)
> Here the drop function was to remove some features that are not needed at the moments. Some of which include ("in_reply_to_status_id", "in_reply_to_user_id", "retweeted_status_id", "retweeted_status_user_id", "retweeted_status_timestamp"). After which we were left with 12 columns to work with.

### Issue #2: Erroneous datatype
> In dealing with erroneous data type the astype function was employed to change datatypes for `timestamp to datetime64` and `name, text, doggo, floofler, pupper, puppo, id_str to string` columns. We succeeded in changing data types for both the `tweet_archieve_clean` data and `tweet_count_clean` datasets.
### Issue #3: Fix column names
> The rename function was applied to change the `id_str` column name in the `tweet_count_clean` dataset to be in line with other id values.
### Issue #4: Lower case names for column name
> For consistency in naming the names on `tweet_archieve_clean` and `image_pred` dataset were made lowercases using the str. lower function

### Issue #5: Mistakes on dog ratings
> Mistakes on dog ratings with indexes `(313, 342, 516, 784, 1068, 1165, 1202, 1662, 2335 for mistaken values)` and `(45, 340, 695, 763, 1689, 1712 for mistakes after decimals)`. It should be noted that most of these values were found during visual cleaning of the datasets on excel. This is because pandas prevent you from viewing the entire data. This was the most exhilarating stage as I was able to find so much mess around the data. Changes were made to the values using the `iloc` function.

### Issue #6: # replace the unidentified names into `none`
> The replace function was called into action again to change values such as `‘a’, ‘all’, ‘an’, ‘by’, ‘his’, ‘just’, ‘my’, ‘not’, ‘such’, ‘the’, ‘this’, ‘very’` to `none` on the name column of the `tweet_archieve_clean` dataset. Again these values were found during visual assessment of the data.
> First a list was created containing the unidentified names then it was pass through a for function to change all values in the list.

### Issue #7: Drop likely predictions that are not true
#### Define:
> It is worthy of note to remember we are dealing with dogs. Any prediction that is not a dog should be droped. The replace function was used to change likely predictions that are not true (meaning they are not dogs) to NAN in the `image_pred` dataset and finally the drop function was used to drop all `NAN` values as we are only interested in dog predictions.
### Issue #8: Clean up text column by taking out the url at the end
> The replace function was also used in this case on the text column using the REGEX notation to replace strings starting with http with an empty space and finally whitespaces were removed using the strip function

### Tidiness Issues
### Issue #9: Clean up text column by taking out the url at the end
>  A new column called rating which is the division(`rating_numerator/rating_denominator`) on the `tweet_archieve_clean` dataset. After this I had to drop some more columns (expanded_urls","rating_numerator","rating_denominator").
*N:B Data Wrangling is iterative*

### Issue #10: Merge the files
> It was important for the `id_str` column to be changed to `tweet_id` for this merge.

> First the `tweet_archieve_clean` and `tweet_count_clean` were merged on the `tweet_id`. Next the resulting dataframe `first_merge` was also merged with `image_pred` on `tweet_id` column.
