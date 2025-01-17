---
title: "The Selenium Browser Automation Project"
---

# The Selenium Browser Automation Project

Selenium is an umbrella project for a range of tools and libraries 
that enable and support the automation of web browsers. 

It provides extensions to emulate user interaction with browsers,
a distribution server for scaling browser allocation,
and the infrastructure for implementations of the 
[W3C WebDriver specification](//www.w3.org/TR/webdriver/)
that lets you write interchangeable code for all major web browsers.

This project is made possible by volunteer contributors
who have put in thousands of hours of their own time,
and made the source code [freely available]({{< ref "/front_matter/copyright_and_attributions.en.md#license" >}})
for anyone to use, enjoy, and improve.

Selenium brings together browser vendors, engineers, and enthusiasts
to further an open discussion around automation of the web platform.
The project organises [an annual conference](//seleniumconf.com/)
to teach and nurture the community.

At the core of Selenium is _[WebDriver]({{< ref "/webdriver/_index.md" >}})_, 
an interface to write instruction sets that can be run interchangeably in many 
browsers. Here is one of the simplest instructions you can make:

{{< code-tab >}}
  {{< code-panel language="java" >}}
import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.WebDriverWait;
import static org.openqa.selenium.support.ui.ExpectedConditions.presenceOfElementLocated;
import java.time.Duration;

public class HelloSelenium {

    public static void main(String[] args) {
        WebDriver driver = new FirefoxDriver();
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
        try {
            driver.get("https://google.com/ncr");
            driver.findElement(By.name("q")).sendKeys("cheese" + Keys.ENTER);
            WebElement firstResult = wait.until(presenceOfElementLocated(By.cssSelector("h3")));
            System.out.println(firstResult.getAttribute("textContent"));
        } finally {
            driver.quit();
        }
    }
}
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support.expected_conditions import presence_of_element_located

#This example requires Selenium WebDriver 3.13 or newer
with webdriver.Firefox() as driver:
    wait = WebDriverWait(driver, 10)
    driver.get("https://google.com/ncr")
    driver.find_element(By.NAME, "q").send_keys("cheese" + Keys.RETURN)
    first_result = wait.until(presence_of_element_located((By.CSS_SELECTOR, "h3>div")))
    print(first_result.get_attribute("textContent"))
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
using System;
using OpenQA.Selenium;
using OpenQA.Selenium.Firefox;
using OpenQA.Selenium.Support.UI;

class HelloSelenium {
  static void Main() {
    using(IWebDriver driver = new FirefoxDriver()) {
      WebDriverWait wait = new WebDriverWait(driver, TimeSpan.FromSeconds(10));
      driver.Navigate().GoToUrl("https://www.google.com/ncr");
      driver.FindElement(By.Name("q")).SendKeys("cheese" + Keys.Enter);
      wait.Until(webDriver => webDriver.FindElement(By.CssSelector("h3")).Displayed);
      IWebElement firstResult = driver.FindElement(By.CssSelector("h3"));
      Console.WriteLine(firstResult.GetAttribute("textContent"));
    }
  }
}
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
require 'selenium-webdriver'

driver = Selenium::WebDriver.for :firefox
wait = Selenium::WebDriver::Wait.new(timeout: 10)

begin
  driver.get 'https://google.com/ncr'
  driver.find_element(name: 'q').send_keys 'cheese', :return
  first_result = wait.until { driver.find_element(css: 'h3>div') }
  puts first_result.attribute('textContent')
ensure
  driver.quit
end
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
const {Builder, By, Key, until} = require('selenium-webdriver');

(async function example() {
    let driver = await new Builder().forBrowser('firefox').build();
    try {
        // Navigate to Url
        await driver.get('https://www.google.com');

        // Enter text "cheese" and perform keyboard action "Enter"
        await driver.findElement(By.name('q')).sendKeys('cheese', Key.ENTER);

        let firstResult = await driver.wait(until.elementLocated(By.css('h3')), 10000);

        console.log(await firstResult.getAttribute('textContent'));
    }
    finally{
        driver.quit();
    }
})();
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
import org.openqa.selenium.By
import org.openqa.selenium.Keys
import org.openqa.selenium.firefox.FirefoxDriver
import org.openqa.selenium.support.ui.ExpectedConditions.presenceOfElementLocated
import org.openqa.selenium.support.ui.WebDriverWait
import java.time.Duration

fun main() {
    val driver = FirefoxDriver()
    val wait = WebDriverWait(driver, Duration.ofSeconds(10))
    try {
        driver.get("https://google.com/ncr")
        driver.findElement(By.name("q")).sendKeys("cheese" + Keys.ENTER)
        val firstResult = wait.until(presenceOfElementLocated(By.cssSelector("h3")))
        println(firstResult.getAttribute("textContent"))
    } finally {
        driver.quit()
    }
}
  {{< / code-panel >}}
{{< / code-tab >}}


See the _[Quick Tour]({{< ref "/getting_started/quick.en.md" >}})_ for a full explanation
of what goes on behind the scenes when you run this code.
You should continue on to the [narrative documentation]({{< ref "/introduction/_index.md" >}})
to understand how you can [install]({{< ref "/selenium_installation/_index.md" >}}) and
successfully use Selenium as a test automation tool,
and scaling simple tests like this to run
in large, distributed environments on multiple browsers,
on several different operating systems.

## Getting started

If you are new to Selenium,
we have a few resources that can help you
get up to speed right away.

* [Quick tour]({{< ref "/getting_started/quick.en.md" >}})
  * [WebDriver]({{< ref "/getting_started/quick.en.md#webdriver" >}})
  * [IDE]({{< ref "/getting_started/quick.en.md#ide" >}})
  * [Grid]({{< ref "/getting_started/quick.en.md#grid" >}})

