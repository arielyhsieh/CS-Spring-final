# Welcome to Ariel's Project

[UML Diagram](https://github.com/arielyhsieh/CS-Spring-final/edit/master/index.md) 

## Superclass Store

```markdown
public class Store 
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
}
```
## Subclass Restaurant

```markdown
import java.util.Scanner;
import java.util.ArrayList;
public class Restaurant extends Store implements Tip
{
    private ArrayList<Order> customerOrders;
    private String[] waiters;
    /*private int customers; 
    private boolean state;*/
    
    public Restaurant()
    {
        super();
        this.customerOrders = new ArrayList<Order>();
        this.customerOrders.add(new Order("chicken", 4.0, "soda", 2));
        this.customerOrders.add(new Order("beef", 2.0, "juice", 2));
        
        this.waiters = new String[3];
        this.waiters[0] = "Bob";
        this.waiters[1] = "Ana";
        this.waiters[2] = "Amy";
        
        /*this.customers = 2;
        
        this.state = true;*/
        
        
    } //end zero arg constructor Restaurant
    public boolean getState() //tells if restaurant is open or closed
    {
        if(customers > 0)
        {
            return true;
        }
        else 
        {
            return false;
        }
    }  //end setter getState   
    public void state() throws Exception
    {
        if(this.customers < 0)
        {
            throw new IllegalArgumentException("The number of customers can't be negative");
        }
        else if(this.customers == 0)
        {
            String output = "Open";
        }
        else
        {
            String output = "Closed";
        }
    }
    public void waiterChange(String newWaiter) //takes a waiter out randomly and puts a new one in
    {
        int index = (int) (Math.random()*waiters.length);
        /*Scanner input = new Scanner(System.in);
        System.out.print("Waiter's name? ");
        newWaiter = input.next();*/
        this.waiters[index] = newWaiter;
    } //end switchWaiter
    public void waiterChange() //a waiter leaves- randomly decided
    {
        int randomWaiter = (int) (Math.random()*waiters.length);
        this.waiters[randomWaiter] = null;
        for(int i = 0; i < waiters.length; i++)
        {
            for (int j = 1; j < waiters.length; j++)
            {
                if (waiters[j-1] == null && waiters[j] != null)//brings the waiters to the front of array, null is at the end of array
                {
                    String index = waiters[j];
                    waiters[j] = waiters[j-1];
                    waiters[j-1] = index;
                }//end if
            }//end nested for loop
        }//end for loop
    } //end waiterLeave
    public int getNumOfWaiters()//calculates the number of waiters
    {
        int numOfWaiters = 0;
        for(int index = 0;index < waiters.length; index++)
        {
            if (waiters[index] != null)
            {
                numOfWaiters ++;
            }//end if
        }//end for
        return numOfWaiters;
    } //end method getNumOfWaiters
    /*public void sortByPrice()
    {
        for(int i = 0; i < this.customerOrders.size() - 1; i++)
        {
            int index = i;
            for(int j = i + 1; i < this.customerOrders.size(); j++)
            {
                if(this.customerOrders.get(j).getDishPrice()+this.customerOrders.get(j).getDrinkPrice() < this.customerOrders.get(index).getDishPrice()+this.customerOrders.get(index).getDrinkPrice())
                {
                    index = j;
                }
            }
            Restaurant small = this.customerOrders.get(index);
            Restaurant big = this.customerOrders.get(i);
            this.customerOrders.remove(i);
            this.customerOrders.remove(index);
            this.customerOrders.add(index, small);
            this.roster.add(i, big);
        }
        
    }*/

    /*public String getSwitchWaiters()
    {
        for (String[] w: waiters)
        {
            this.waiters = w ;
        }
        return this.waiters;
    }*/
    public void customerLeave()//tracks the number of customers, removes them from ArrayList
    {
        this.customerOrders.remove(1);
        this.customers -= 1;
    } //end customerLeave
    public void customerArrive()//asks for input of order when customers arrive
    {
        Scanner input = new Scanner(System.in);
        System.out.println("Do you want chicken or beef?");
        String dish = input.next();
        System.out.println("How many would you like?");
        int dishCount = input.nextInt();
        System.out.println("Do you want soda or juice?");
        String drink = input.next();
        System.out.println("How many would you like?");
        int drinkCount = input.nextInt();
        this.customerOrders.add(new Order(dish, dishCount, drink, drinkCount));
        this.customers += 1;
    } //end customerArrive
    public int getCustomerCount()//gets the number of customers
    {
        return customers;
    } //end method getCustomerCount
    public String getDiscount(int index)//subtracts 3 if total price is over 15 or customer orders 2 of a dish and drink
    {
        double discount = 0;
        double total = 0;
         /*for (int index = 0; index < customerOrders.size() ; index++)
        {*/
            if (this.customerOrders.get(index).getDishPrice()+this.customerOrders.get(index).getDrinkPrice() > 15)
            {
                discount = 3;
            }//discount if total price is above 15
            else if ((this.customerOrders.get(index).getDishPrice() == 10.0 || this.customerOrders.get(index).getDishPrice() == 12.0) && (this.customerOrders.get(index).getDrinkPrice() == 2.0 || this.customerOrders.get(index).getDrinkPrice() == 4.0))
            {
                discount = 3;
            }//discount if order 2 of the same dish and 2 of the same drink
            total = this.customerOrders.get(index).getDishPrice()+this.customerOrders.get(index).getDrinkPrice()-discount;
            return "Discount: " + discount + "\nNew Total: " + total;
    } //end method getDiscount
    
    public String toString()//prints out the waiters working, each customer's order, total price before and after discount, and number of customers
    {
        String orderOutput = new String();
        
        if(this.state == true)
        {
            orderOutput += "\nThe restaurant is open!";
            orderOutput += "\n\nWaiters: ";
            for(String allWaiters : waiters)
            {
                orderOutput += allWaiters + ", ";
            }//end for-each
            for(int index = 0; index < customerOrders.size(); index++)
            {
                orderOutput += "\n\n" + "Order " + (index+1) + "\n" + customerOrders.get(index);
                if (this.customerOrders.get(index).getDishPrice()+this.customerOrders.get(index).getDrinkPrice() > 15)
                {
                    orderOutput = orderOutput + getDiscount(index);
                }
            }//end for
        }//end if statement
        else
        {
           orderOutput = "\n\nThe restaurant is closed!";
        }//end else
    
        return orderOutput;
    } //end method toString
    public void tip()
    {
        System.out.println("Fast service-tip");
    }
    public void noTip()
    {
        System.out.println("Slow service-no tip");
    }
}
```
## Restaurant Driver

```markdown
import java.util.Scanner;
public class RestaurantDriver
{
    public static void main(String[] args)
    {
        Restaurant restaurant = new Restaurant();
        
        while (restaurant.getCustomerCount() < 3)//ensures that only 4 customers can be in the restaurant 
        {
            restaurant.customerArrive();
            restaurant.tip();
        }//end while
        Scanner input = new Scanner(System.in);
        System.out.print("Waiter's name? ");
        String newWaiter = input.next();
        restaurant.waiterChange(newWaiter);//switching out a waiter for another
        
        do//ensures that there are at least 2 waiters working
        {
            restaurant.waiterChange();
        }
        while(restaurant.getNumOfWaiters() > 2);//end do-while
        String name = "The Fancy Restaurant";
        String newName = name.substring(4,9);
        String newName2 = ", the Restaurant";
        System.out.println("\n\n" + "\"" + newName.concat(newName2) + "\"");//the restaurant changed its name
        System.out.println(restaurant + "\n\nNumber of customers: " + restaurant.getCustomerCount());
    }//end main method
}//end class RestaurantDriver
            
```
## Subclass Bakery

```markdown
public class Bakery extends Store implements Tip
{
    private int cakeAmt;
    private int cupcakeAmt;
    
    public Bakery()
    {
        super();
        this.cakeAmt = 2;
        this.cupcakeAmt = 24;
    }
    public Bakery(int customers, boolean state, int cakeAmt, int cupcakeAmt)
    {
        super(customers, state);
        this.cakeAmt = cakeAmt;
        this.cupcakeAmt = cupcakeAmt;
    }
    public int getCakeAmt()
    {
        return cakeAmt;
    }
    public void setCakePrice(int cakeAmt)
    {
        this.cakeAmt = cakeAmt;
    }
    public double getCakePrice()
    {
        double cakePrice = 20.0*cakeAmt;
        return cakePrice;
    }
    public int getCupcakeAmt()
    {
        return this.cupcakeAmt;
    }
    public void setCupcakePrice(int cupcakeAmt)
    {
        this.cupcakeAmt = cupcakeAmt;
    }
    public double getCupcakePrice()
    {
        double cupcakePrice = 3.0*cupcakeAmt;
        return cupcakePrice;
    }
    public String toString()
    {
        double total = getCakePrice() + getCupcakePrice();
        String orderOutput = "\nNumber of cakes: " + getCakeAmt() + "\tPrice: " + getCakePrice() + "\tNumber of cupcakes: " + cupcakeAmt + "\tPrice: " + getCupcakePrice() + "\nTotal: " + total;
        return orderOutput;
    }
    public void tip()
    {
        System.out.println("Good service-tip");
    }
    public void noTip()
    {
        System.out.println("Bad service-no tip");
    }
    public void restock()
    {
        System.out.println("restock the ingredients");
    }
}
```
## Bakery Driver

```markdown
public class BakeryDriver
{
    public static void main(String[] args)
    {
        Bakery bakery1 = new Bakery();
        Bakery bakery2 = new Bakery(2, true, 3, 12);
        Store bakery3 = new Bakery();
        bakery3.restock();
        System.out.println(bakery1);
        bakery1.tip();
        System.out.println(bakery2);
        bakery2.tip();
    }
}
```
## Interface Tip

```markdown
public interface Tip
{
    abstract void tip();
    abstract void noTip();
}

```

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
