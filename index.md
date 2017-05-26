## Welcome to Ariel's Project

You can use the [editor on GitHub](https://github.com/arielyhsieh/CS-Spring-final/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Code

Superclass Store

```markdown
'public class Store 
{
    int customers;
    boolean state;
    
    public Store()
    {
        this.customers = 2;
        this.state = true;
    }
    public Store(int customers, boolean state)
    {
        customers = customers;
        state = state;
    }
    public int getCustomers()
    {
        return customers;
    }
    public boolean isClosed()
    {
        return false;
    }
    public void restock()
    {
        System.out.println("restock the supplies");
    }
    public String toString()
    {
        String output = new String();
        output = "There are " + customers + "customers in the store.";
        return output;
    }
}'
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/arielyhsieh/CS-Spring-final/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
