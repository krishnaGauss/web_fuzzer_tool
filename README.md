# Fuzzer_Buzzer

## General info
> Simple Web Fuzzer
  1. **Crawling** : Collects All Internal URL ( [Crawler.py](https://github.com/mheidari98/Web-Fuzzer/blob/main/Wuzzer/Crawler.py) )
  2. Uses **Selenium** And **BeautifulSoup** to Detect Form & Input Params For Fuzzing
  3. Injects Payloads
  4. Checks Responses to Detect Vulnerabilities
---

## Requirements
- Python3
- Use Virtual Environments & Install Requirements Packages ([gist](https://gist.github.com/mheidari98/8ae29b88bd98f8f59828b0ec112811e7)) 
- Chrome Web Driver : Download It From The Address Below And Put It in The **Wuzzer** Folder
  ```
  Chrome:    https://sites.google.com/a/chromium.org/chromedriver/downloads
  ```

 ---

## Usage
  For Test on DVWA :
  ```bash
  cd Wuzzer
  python Wuzzer.py --test --XSSi --SQLi --BSQLi --CMDi --BCMDi 
  ```
  For More Options :
  ```bash
  python Wuzzer.py -h
  ```

---

## Test on [DVWA Docker](https://hub.docker.com/r/vulnerables/web-dvwa/)  
  + Run Image
    ```bash
    docker run --rm -it -p 80:80 vulnerables/web-dvwa
    ```
  + Database Setup
    > http://127.0.0.1/setup.php
  + Login with Default Credentials
    - Username: **admin**
    - Password: **password**

---

## Task-Lists
- [x] Xss Injection Attack
- [x] SQL Injection Attack
- [x] Blind SQL Injection Attack
- [x] Command Injection Attack
- [x] Blind Command Injection Attack
- [ ] Complete Document
- [ ] Threading Support
- [ ] Use Proxy

--------------------------------------------------------------------------------------------------------------------------------

# Web Fuzzing Tool
![python version](https://img.shields.io/github/pipenv/locked/python-version/hadiMh/selenium_fuzzer?color=2196F3&logo=python&logoColor=white)
![selenium version](https://img.shields.io/badge/dynamic/json?color=2196F3&label=Selenium&query=%24.default.selenium.version&url=https%3A%2F%2Fraw.githubusercontent.com%2FhadiMh%2Fselenium_fuzzer%2Fmain%2FPipfile.lock&logo=Selenium&logoColor=white)
![code size](https://img.shields.io/github/languages/code-size/hadiMh/selenium_fuzzer?color=2196F3)

This tool is for finding XSS vulnerabilities on websites. It gets the website url, the login credentials if needed and the urls to exclude and then starts to crawl the website to find any XSS vulnerabilities.

It uses Selenium as the Scraping tool.

## How to run the app

1. Using Pipenv (recommended)

    First install the [Pipenv](https://pipenv.pypa.io) by this command:

    ```console
    $ pip install pipenv
    ```

    Then clone the project to your local machine.

    ```console
    $ git clone https://github.com/krishnaGauss/fuzzer_buzzer/selenium_fuzzer.git
    ```

    Then install the required packages with the command below:

    ```console
    $ pipenv install
    ```

    And you are good to go :)

2. Using virtualenv

    First install virtualenv by this command:

    ```console
    $ pip install virtualenv
    ```

    Then clone the project to your local machine.

    ```console
    $ git clone https://github.com/hadiMh/selenium_fuzzer.git
    ```

    Then create the virtual environment in the project folder:

    This will create a venv folder in your project and then activates it.

    ```console
    $ virtualenv venv
    $ source venv/bin/activate
    ```

    Then install the required packages with the command below:

    ```console
    (venv) $ pip install -r requirements.txt
    ```
# Usage

The only step needed is to run the UI of the app.
At the root directory of the project run:
```console
$ python3 app_interface.py
```

The above code will run the program below:

![image of fuzzing tool main UI empty fields](https://user-images.githubusercontent.com/36237368/127186920-6480c1db-d7c0-4dc4-8eb1-561dc8e74ad9.png)



# Usage Steps

( You will see each step UI section after this part )

1. Enter the Url of a page of the website.

2. If it needs to login, enter the credentials and the login url on the right.
3. Enter all the urls to exclude from being scraped by entering them in the "Urls to Exclude" textarea. (separate each url with new line)
4. Click on the "Find Urls of This Website. It will collect all the urls of the website.
5. After it finished, Click on the "Get Forms". It will collect all the urls of the previous step that contains at least one form.
6. After the last step finished click on the "Perform XSS Check". It will check all the urls of the previous step (they all contain at least one form) and check for XSS vulnerability of all the forms.
7. The vulnerable forms get printed with their url and form method on the list.



# How to use the app by details

![](https://user-images.githubusercontent.com/36237368/127187507-ee7bc05e-de54-4f81-8689-ef8eceae2248.png)

1. Enter the url of a webpage of the target website.
    - You can check the correctness of the url with the "Check URL" button on the right.

    - It is arbitrary for the Url to contain `http://`, `https://` or `www.`

2. Login Credentials section.
    - If you want the crawler to login to the website before start crawling, you can use this section. **Otherwise leave it empty**.

    - If this section is used, the crawler will first login with the specified credentials to the specified login url and the starts crawling.
    - You can also login manually. To do so just click on the "Open Browser" below the login section. Then navigate to the webpage you want and login manually. 
        - Remember you have to keep the browser open to keep the already logged in session.

3. Black list urls section.
    - If you don't want to visit some urls of the website, specify them here.

    - It's necessary to add the `logout` url to the list if you are using the login section to login to the website.
     Otherwise the crawler will visit the `logout` url and logs out in the middle of the crawling.
    - Separate urls with `new line`.

4. Start Crawling.
    - After entering the website url (necessary), login credentials (optional) and black list urls (optional) you are ready to start crawling.

    - By clicking on "Find Urls of This Website" the crawler will open the browser (or use the already opened browser) to start finding all the urls of the website.
    - This process will take time so be patient.
    - All the found urls are going to be shown in the list view in the app as the crawler is running. (MultiThreading)
    - As mentioned briefly in the previous sections, all the found urls are being saved in a file too. The file is located at `saved_data/all_explored_urls.txt`. This file will be used for the further steps if you have closed the app and try to continue the work to the next steps.
    - Remember this file will be overwritten if you click on the "Find Urls of This Website" because it will start crawling to find urls based on the new input.

5. After that all the urls of the website are found, it's time to find all the forms of all the urls. So now click on the "Get Forms" button.
    - It starts to explore all the found urls in previous section. But this time it will filter all the urls that contain form tags.

    - The result of this process is all the urls that contain at least one form
    - You can see the filtered urls simultaneously in the list view of the app. It prints the details of the filtered urls.
    - The columns of the output are:
        1. Id: the number of the row
        2. Full Url: the url of the page that contains form
        3. Num: the number of the form in the page. For example if it is about the second form of 3 forms on this url page it will be equal 2/3.
        4. Method: The form method (eg. GET/POST)
        5. Xss: this field is empty now. It will be populated in the next step.

6. So until now we have all the urls of this website that we now there is at least one form on that page. Now it's time to perform XSS attack on all these forms to find potential vulnerabilities.
To do so click on "Perform XSS Attack".
    - It uses the found urls in the last step.

    - It performs XSS attack by html tags to find potential vulnerabilities.
    - Urls that contain XSS vulnerability get printed in the list view in the UI.
    - The column "Xss" that I said is empty in the previous step, gets the value True if the XSS attack was successful.

---

## Notes:

1. Notice that each step results are getting saved on files for further usage (in saved_data directory).
    - All the urls of the website are saved in the `saved_data/all_explored_urls.txt` file.
    - All the urls that contain at least one form are saved in `saved_data/urls_with_form.txt`

2. You can use "Load" checkboxes to load urls from the saved files of previous runs.
    - To load the already found urls just check the `Load urls from file` checkbox and then click on the `Find Urls of This Website` button. It will load the data from the `saved_data/all_explored_urls.txt` file instead of live crawling.

    - To load the already found urls that contain at least one form, just check the `Load form urls from file` checkbox and then click on the `Get Forms` button. It will load the data from the `saved_data/urls_with_form.txt` file instead of live crawling.

3. You can login manually by clicking on the "Login manually: Open Browser" button.
    - After you logged in manually click on any of the previous steps but DO NOT close the browser because the already logged in session will be gone.

4. If you are using login section, remember to enter the logout url in to "Urls to Exclude" to stop the scraper from logging out.

5. You can check the entered url correctness by clicking on the "Check URL" button.

--------------------------------------------------------------------------------------------------------------------------------

# Dom_checker
#### A DOM fuzzer

A basic DOM objects checker and vulnerability detection script for web pages.

#### Usage

To see the usage information run the following command:

`python3 generator.py --help`

To generate a single .html sample run:

`python generator.py --file <output file>`

To generate a single .html sample run using a template you wrote:

`python generator.py --file <output file> --template <your custom template file>`

To generate multiple samples with a single call run:

`python generator.py --output_dir <output directory> --no_of_files <number of output files>`

The generated samples will be placed in the specified directory and will be named as fuzz-&lt;number&gt;.html, e.g. fuzz-00001.html, fuzz-00002.html etc. Generating multiple samples is faster because the input grammar files need to be loaded and parsed only once.

#### Code organization

generator.py contains the main script. It uses grammar.py as a library and contains additional helper code for DOM fuzzing.

grammar.py contains the generation engine that is mostly application-agnostic and can thus be used in other (i.e. non-DOM) generation-based fuzzers. As it can be used as a library, its usage is described in a separate section below.

.txt files contain grammar definitions. There are 3 main files, html.txt, css.txt and js.txt which contain HTML, CSS and JavaScript grammars, respectively. These root grammar files may include content from other files.

#### Using the generation engine and writing grammars

To use the generation engine with a custom grammar, you can use the following python code:

```
from grammar import Grammar

my_grammar = Grammar()
my_grammar.parse_from_file('input_file.txt')
result_string = my_grammar.generate_symbol('symbol_name')

```

The following sections describe the syntax of the grammar files.

##### Basic syntax

Domato is based on an engine that, given a context-free grammar in a simple format specified below, generates samples from that grammar.

A grammar is described as a set of rules in the following basic format:

`<symbol> = a mix of constants and <other_symbol>s`

Each grammar rule contains a left side and the right side separated by the equal character. The left side contains a symbol, while the right side contains the details on how that symbol may be expanded. When expanding a symbol, all symbols on the right-hand side are expanded recursively while everything that is not a symbol is simply copied to the output. Note that a single rule can't span over multiple lines of the input file.

Consider the following simplified example of a part of the CSS grammar:

```
<cssrule> = <selector> { <declaration> }
<selector> = a
<selector> = b
<declaration> = width:100%
```

If we instruct the grammar engine to parse that grammar and generate 'cssrule', we may end up with either:

`a { width:100% }`

or

`b { width:100% }`

Note there are two rules for the 'selector' symbol. In such cases, when the generator is asked to generate a 'selector', it will select the rule to use at random. It is also possible to specify the probability of the rule using the 'p' attribute, for example:

```
<selector p=0.9> = a
<selector p=0.1> = b
```

In this case, the string 'a' would be output more often than 'b'.

There are other attributes that can be applied to symbols in addition to the probability. Those are listed in a separate section.

Consider another example for generating html samples:

```
<html> = <lt>html<gt><head><body><lt>/html<gt>
<head> = <lt>head<gt>...<lt>/head<gt>
<body> = <lt>body<gt>...<lt>/body<gt>
```

Note that since the '<' and '>' have a special meaning in the grammar syntax, so here we are using `<lt>` and `<gt>` instead. These symbols are built in and don't need to be defined by the user. A list of all built-in symbols is provided in a separate section.

##### Generating programming language code

To generate programming language code, a similar syntax can be used, but there are a couple of differences. Each line of the programming language grammar is going to correspond to the line of the output. Because of that, the grammar syntax is going to be more free-form to allow expressing constructs in various programming languages. Secondly, when a line is generated, in addition to outputting the line, one or more variables may be created and those variables may be reused when generating other lines. Again, let's take a look of the simplified example:

```
!varformat fuzzvar%05d
!lineguard try { <line> } catch(e) {}

!begin lines
<new element> = document.getElementById("<string min=97 max=122>");
<element>.doSomething();
!end lines
```

If we instruct the engine to generate 5 lines, we may end up with something like:

```
try { var00001 = document.getElementById("hw"); } catch(e) {}
try { var00001.doSomething(); } catch(e) {}
try { var00002 = document.getElementById("feezcqbndf"); } catch(e) {}
try { var00002.doSomething(); } catch(e) {}
try { var00001.doSomething(); } catch(e) {}
```

Note that

- programming language lines are enclosed in '!begin lines' and '!end lines' statement. This gives the grammar parser the necessary information that the lines in-between are programming language lines and are thus parsed differently.
- We used `<new element>` instead of `<element>`. This instructs the generator to create a new variable of type 'element' instead of generating the 'element' symbol.
- `<string>` is one of the built-in symbols so no need to define it.
- [optional] You can use !varformat statement to define the format of variables you want to use.
- [optional] You can use !lineguard statement to define additional code that gets inserted around every line in order to catch exceptions or perform other tasks. This is so you wouldn't need to write it for every line separately.
- In addition to '!begin lines' and '!end lines' you can also use '!begin helperlines' and '!end helperlines' to define lines of code that will only ever be used if required when generating other lines (for example, helper lines might generate variables needed by the 'main' code, but you don't ever want those helper lines to end up in the output when they are not needed).

##### Comments

Everything after the first '#' character on the line is considered a comment, so for example:

```
#This is a comment
```


##### Preventing infinite recursions

The grammar syntax has a way of telling the fuzzer which rules are nonrecursive and can be safe to use even if the maximum level of recursion has been reached. This is done with the ‘nonrecursive’ attributes. An example is given below.

```
!max_recursion 10
<test root=true> = <foobar>
<foobar> = foo<foobar>
<foobar nonrecursive> = bar
```

Firstly, an optional ‘!max_recursion’ statement defines the maximum recursion depth level (50 by default). Notice that the second production rule for ‘foobar’ is marked as non-recursive. If ever the maximum recursion level is reached the generator will force using the non-recursive rule for ‘foobar’ symbol, thus preventing infinite recursion.

##### Including and importing other grammar files

In Domato, including and importing grammars are two different context.

Including is simpler. You can use:

```
!include other.txt
```

to include rules from other.txt into the currently parsed grammar.

Importing works a bit differently:

```
!import other.txt
```

tells the parser to create a new Grammar() object that can then be referenced from the current grammar by using the special `<import>` symbol, for example like this:

```
<cssrule> = <import from=css.txt symbol=rule>
```

You can think about importing and including in terms of namespaces: !include will put the included grammar into the single namespace, while !import will create a new namespace which can then be accessed using the `<import>` symbol and the namespace specified via the 'from' attribute.













