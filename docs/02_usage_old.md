# Using Bergwerk

## Creating or editing chatbot content

### Page structure

This is the source code of the "Start" page of a fresh Bergwerk installation. 
The "Start" page is the first page that is displayed if the user accepted the 
ToS of the chatbot. You can access the page at 
`http://localhost/wiki/w/index.php?title=Start`.

- The start page is the first outputted page after the user accepts the ToS. 
- You can link to other pages, and every output of the chatbot contains a button that leads to the "Home" page (in case you want specific instructions on the start page, which is displayed only once.)
- All Chatbot content pages should have the [[Category:Content]] tag. This ensures that they are included in the intent classifier training and are included at export time.
- The content of the chtabot can be seen as  a hierarchichal tree structure. 

### Chatbot answers

- The Chatbot answers are divided into two main sections, "= English =" and "= German ="
- The subsections "== Markdown ==" of each language provide the output of the chatbot in the respective language. 
- You can also add <markdown> and </markdown> tags so that your markdown is rendered directly within the wiki. 
- However, it is not necessary to add them for the webchat plugin. 

### Chatbot buttons

- When you add a "== Buttons ==" subsection to a specific langauge, you can insert buttons that the user can click on. 
- You can add Links to the content of other wiki pages by adding links to other wiki pages. This is done by using the standard wikitext link format `[[Page title in Wiki|Button Text]]`
- Each example should begin with an "*", followed by a whitespace. 


### Training questions 

- In order to train the intent classifier, you have to add example questions that could lead to this page, if possible, use te least 10 English and German sentences each. 
- Each example should begin with an "*", followed by a whitespace. 

## Admin functions

- Wiki Structure
- Page: Deutsch / English / Markdown / Training Questions- 
- Menu Buttons
- Categories
- Training Questions
- Intent Classifier 
- Import Export
