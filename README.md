# Simon-Lights
The Simon memorization game, built from the ground up.

Notes:
Meta
<meta> is data about data. 
Has to be declared in the <head> </head> element, and tells the computer information about the webpage. Some useful <meta> tags are:
<meta charset=”UTF-8”>  <!-- the type of characters used, such as ASCII →
<meta name=”viewport” content=”width=device-width, initial-scale=1.0”> <!-- scales proportionately when viewing a website on a mobile device →

Td, Tr
<tr> </tr> is for creating rows of cells in a table. <td> </td> is for creating columns in a table. 
Example:
<!DOCTYPE html>  
<html>  
<head>  
    <title>HTML td tag</title>  
    <style>  
    th{  
     background-color: #6495ed;  
    }  
    th,td{  
        border: 1px solid black;  
        padding: 10px;  
        }  
    </style>  
</head>  
<body>  
  <h2>Example of td Tag</h2>  
  <table style=" border-collapse: collapse; background-color:#dcdcdc;">  
       <tr>  
    <th>Product</th>  
    <th>Quantity</th>  
    <th>Price</th>  
       </tr>  
  
    <tr>  
        <td>Books</td>    
        <td>5</td>  
         <td>589</td>  
    </tr>  
  
    <tr>  
       <td>T-shirt</td>   
       <td>5</td>  
       <td>3500</td>  
    </tr>  
              
            <tr>  
      <td>Jeans</td>      
        <td>2</td>  
       <td>5000</td>  
    </tr>  
  </table>  
</body>  
</html>  


For more info, see: https://www.javatpoint.com/html-td-tag#:~:text=HTML%20%3Ctd%3E%20tag%20is%20used%20to%20specify%20the,table%20row%20can%20contain%20multiple%20%3Ctd%3E%20data%20elements.
Making shapes info:
[SVG Path (w3schools.com)](https://www.w3schools.com/graphics/svg_path.asp)



**
Deploying a file**
Create a file called deployFiles.sh and add it to your project.

Add the following code to the file:

#!/bin/bash


while getopts k:h:s: flag


do


   case "${flag}" in


       k) key=${OPTARG};;


       h) hostname=${OPTARG};;


       s) service=${OPTARG};;


   esac


done


if [[ -z "$key" || -z "$hostname" || -z "$service" ]]; then


   printf "\nMissing required parameter.\n"


   printf "  syntax: deployFiles.sh -k <pem key file> -h <hostname> -s <service>\n\n"


   exit 1


fi


printf "\n----> Deploying files for $service to $hostname with $key\n"


# Step 1


printf "\n----> Clear out the previous distribution on the target.\n"


ssh -i "$key" ubuntu@$hostname << ENDSSH


rm -rf services/${service}/public


mkdir -p services/${service}/public


ENDSSH


# Step 2


printf "\n----> Copy the distribution package to the target.\n"


scp -r -i "$key" * ubuntu@$hostname:services/$service/public

Lastly in your terminal, type ./deployFiles.sh -k ~/keys/Securitykey.pem -h yourdomain.click -s simon
//the -s simon is an example of a root to the website. For example, this would show up as Simon-lights (worldwideunified.org)

Don’t forget to call the main html file as index.html, otherwise the website won’t know where to start.


