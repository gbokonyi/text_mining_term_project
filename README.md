# Data Science on Unstructured Text Data - Term Project

## *Learning a language takes time and patience, but some text mining can help.*

As I was studing a foreign language, I was always wondering which words are the most "useful" to learn first, that come up frequently in texts. My project idea was to create a word count on texts originating from the web, that shows word occurencies and give indication which words shall a student focus on to learn in order to be able to understand the content. 

As I was studying german before as a foreign language and I'm also interested in economics, I choose the Fazit blog as a source material (http://blogs.faz.net/fazit/), the economics related blog of Frankfurter Allgemeine Zeitung.

I wanted my corpus to contain multiple blogposts, so first I needed a web crawler package in R, that helps with gathering the URLs that need to be parsed. Fortunately I have found one on CRAN: the package is called Rcrawler. I used the posts of 2017 from the blog, the package made it possible with some regex based filtering that I could keep only the needed URL addresses. Crawling through the URLs it turned out, that some of the posts have multiple pages because of the comment sections, so I had to clean the url table a bit, I did this with the stringr package.

Once a data frame was ready with the relevant URLs, I was able to parse the blogposts and save the text content with the rvest package, and create a dataset that contains the corpus. Data cleaning seems to be particularily difficult with text coming from the web. I did some cleaning by trying to exclude all the repeating lines which contained the links to other articles, and some other html lines. After that I could unnest tokens, remove the stopwords and do the actual wordcount. 

The top 10 used words were these:

1.  dass	      1067			
2.  mehr	      393			
3.  geld	      390			
4.  the	        373			
5.  gibt	      331			
6.  immer	      325			
7.  of	        298			
8.  banken	    275			
9.  ja	        273			
10. schon       272

The first word is unfortunately a stopword, but the stopword dictionary contained it with a different ortography, using a special charater ("ß"). It also seems that the corpus contains english text as well, direct quotations from books written in english, so I have to clean these features too.

Even in this state we could visualise Zipf's law though: 

![alt text](https://github.com/gbokonyi/text_mining_term_project/blob/master/plot_zipf.png)

After the last data cleaning, the top 10 used words were these:

1.  geld	      390	
2.  gibt	      331	
3.  immer	      325	
4.  banken	    275	
5.  schon	      272
6.  jahren	    245
7.  ökonomen	  229	
8.  unternehmen	214	
9.  bank	      201		
10. geldpolitik	190


The outcome is not so surprising: geld (money) is at the first place, as we would expect from an economics related blog. Also made to the top 10: bank / banken (banks), ökonomen (economists), unternehmen (enterprises) and geldpolitik (monetary policy).

The final version of the Zipf's law plot looks like this:

![alt text](https://github.com/gbokonyi/text_mining_term_project/blob/master/plot_zipf2.png)



