---
description: >-
  The steps taken to calculate a Parliamentary Attendance Rating (PAR) Score for
  ranking members of parliament (MPs) according to their attendance across
  portfolio committee meetings.
icon: scale-balanced
cover: >-
  https://images.unsplash.com/photo-1554007460-791a7b8945d8?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw0fHxQYXJsaWFtZW50fGVufDB8fHx8MTcyNTM2MTE1OHww&ixlib=rb-4.0.3&q=85
coverY: 0
---

# PAR Score Methodology

## The data we have

We have the following data for MP attendance at portfolio committee meetings throughout the year:

* Column A = <mark style="color:red;">**id**</mark> — Unique number assigned to each MP (e.g., _1423_)
* Column B = <mark style="color:red;">**member\_name**</mark> — Surname and initials of an MP (e.g., _Hendricks, Mr MGE_)
* Column C = <mark style="color:red;">**party\_name**</mark> — Political party an MP is representing (e.g., _Al Jama-ah_)
* Column D = <mark style="color:red;">**date\_created**</mark> — Date a portfolio committee meeting took place (e.g., _06/02/2024_)
* Column E = <mark style="color:red;">**year**</mark> — Year a portfolio committee meeting took place (e.g., _2024_)
* Column F = <mark style="color:red;">**attendance**</mark> — Attendance of an MP at a portfolio committee meeting (e.g., _Absent_)
* Column G = <mark style="color:red;">**committee\_meeting**</mark> — The Portfolio Committee meeting (e.g., _International Relations_)

## What we are trying to achieve

We want to be able to <mark style="color:red;">**rank MPs based on their attendance across all portfolio committee meetings**</mark> throughout a year, taking into account the total number of portfolio committees they are subscribed to for that year. To do this, we need to extract the following from the data we have:

1. No. of times an MP was _<mark style="color:red;">**Absent**</mark>_ for meetings throughout a year.
2. No. of times an MP was _<mark style="color:red;">**Absent with Apologies**</mark>_ for meetings throughout a year.
3. No. of times an MP _<mark style="color:red;">**Arrived Late**</mark>_ for meetings throughout a year.
4. No. of times an MP _<mark style="color:red;">**Arrived Late & Departed Early**</mark>_ from meetings throughout a year.
5. No. of times an MP _<mark style="color:red;">**Departed Early**</mark>_ from meetings throughout a year.
6. No. of times an MP was _<mark style="color:red;">**Present**</mark>_ for meetings throughout a year.
7. No. of _<mark style="color:red;">**Unique Portfolio Committees**</mark>_ an MP is subscribed to throughout a year.
8. _<mark style="color:red;">**Average**</mark>_ no. of _<mark style="color:red;">**Unique Portfolio Committees per MP**</mark>_ throughout a year.

In addition to extracting the data points above, we assign weightings to the different types of attendance, as follows:

* <mark style="color:red;">**0.0**</mark> for _Absent_
* <mark style="color:red;">**0.25**</mark> for _Absent with Apologies_
* <mark style="color:red;">**0.75**</mark> for _Arrived Late_
* <mark style="color:red;">**0.5**</mark> for _Arrived Late & Departed Early_
* <mark style="color:red;">**0.75**</mark> for _Departed Early_
* <mark style="color:red;">**1.0**</mark> for _Present_

Below are the steps for extracting each of the numbered bullet points above, and calculating a Parliamentary Attendance Rating (PAR) score for each MP in a given year.

<mark style="color:red;">**NOTE:**</mark> These steps apply to Google Sheets.

## <mark style="color:red;">STEP 1</mark> — Extracting the <mark style="color:red;">Absent</mark> count per MP

Assuming our first row is a header row, we use the following formula in cell H2:

{% hint style="info" %}
\=COUNTIFS(B:B, B2, E:E, E2, F:F, "Absent")
{% endhint %}

Where:

* Column B = **member\_name**
* Column E = **year**
* Column F = **attendance**

We drag this formula down Column H, and label it <mark style="color:red;">**absent\_count**</mark>.

## <mark style="color:red;">STEP 2</mark> — Extracting the <mark style="color:red;">Absent with Apologies</mark> count per MP

Assuming our first row is a header row, we use the following formula in cell I2:

{% hint style="info" %}
\=COUNTIFS(B:B, B2, E:E, E2, F:F, "Absent with Apologies")
{% endhint %}

Where:

* Column B = **member\_name**
* Column E = **year**
* Column F = **attendance**

We drag this formula down Column I, and label it <mark style="color:red;">**absent\_with\_apologies\_count**</mark>.

## <mark style="color:red;">STEP 3</mark> — Extracting the <mark style="color:red;">Arrived Late</mark> count per MP

Assuming our first row is a header row, we use the following formula in cell J2:

{% hint style="info" %}
\=COUNTIFS(B:B, B2, E:E, E2, F:F, "Arrived Late")
{% endhint %}

Where:

* Column B = **member\_name**
* Column E = **year**
* Column F = **attendance**

We drag this formula down Column J, and label it <mark style="color:red;">**arrived\_late\_count**</mark>.

## <mark style="color:red;">STEP 4</mark> — Extracting the <mark style="color:red;">Arrived Late & Departed Early</mark> count per MP

Assuming our first row is a header row, we use the following formula in cell K2:

{% hint style="info" %}
\=COUNTIFS(B:B, B2, E:E, E2, F:F, "Arrived Late & Departed Early")
{% endhint %}

Where:

* Column B = **member\_name**
* Column E = **year**
* Column F = **attendance**

We drag this formula down Column K, and label it <mark style="color:red;">**arrived\_late\_departed\_early\_count**</mark>.

## <mark style="color:red;">STEP 5</mark> — Extracting the <mark style="color:red;">Departed Early</mark> count per MP

Assuming our first row is a header row, we use the following formula in cell L2:

{% hint style="info" %}
\=COUNTIFS(B:B, B2, E:E, E2, F:F, "Departed Early")
{% endhint %}

Where:

* Column B = **member\_name**
* Column E = **year**
* Column F = **attendance**

We drag this formula down Column L, and label it <mark style="color:red;">**departed\_early\_count**</mark>.

## <mark style="color:red;">STEP 6</mark> — Extracting the <mark style="color:red;">Present</mark> count per MP

Assuming our first row is a header row, we use the following formula in cell M2:

{% hint style="info" %}
\=COUNTIFS(B:B, B2, E:E, E2, F:F, "Present")
{% endhint %}

Where:

* Column B = **member\_name**
* Column E = **year**
* Column F = **attendance**

We drag this formula down Column M, and label it <mark style="color:red;">**present\_count**</mark>.

## <mark style="color:red;">STEP 7</mark> — Calculating a <mark style="color:red;">Weighted Attendance Score</mark> per MP

With the attendance data extracted, and the weightings assigned earlier, we can calculate a Weighted Attendance Score per MP, for a given year, using the following formula in cell N2:

{% hint style="info" %}
\=(H20)+(I20.25)+(J20.75)+(K20.5)+(L20.75)+(M21)
{% endhint %}

Where:

* Column H = **absent\_count**
* Column I = **absent\_with\_apologies\_count**
* Column J = **arrived\_late\_count**
* Column K = **arrived\_late\_departed\_early\_count**
* Column L = **departed\_early\_count**
* Column M = **present\_count**

We drag this formula down Column N, and label it <mark style="color:red;">**weighted\_attendance\_score**</mark>.

## <mark style="color:red;">STEP 8</mark> — Extracting <mark style="color:red;">Unique Portfolio Committees</mark> count per MP

To extract the number of unique portfolio committees an MP is subscribed to throughout a year, we first need to create a ‘helper’ column. We do this using the following formula in cell O2:

{% hint style="info" %}
\=UNIQUE(B2:B & “-” & E2:E)
{% endhint %}

Where:

* Column B = **member\_name**
* Column E = **year**

We drag this formula down Column O, and label it <mark style="color:red;">**helper\_column**</mark>.

This creates a unique combination of **member\_name** and **year** in Column O. We can use this unique combination to extract the number of unique portfolio committees a member is subscribed to for a given year, using the following formula in cell P2:

{% hint style="info" %}
\=COUNTA(UNIQUE(FILTER(G2:G, B2:B & “-” & E2:E = O2)))
{% endhint %}

Where:

* Column B = **member\_name**
* Column E = **year**
* Column G = **committee\_meeting**

We drag this formula down Column P, and label it <mark style="color:red;">**unique\_committee\_count\_per\_member\_for\_year**</mark>.

## <mark style="color:red;">STEP 9</mark> — Extracting <mark style="color:red;">Average</mark> <mark style="color:red;">Unique Portfolio Committees</mark> per MP

Calculate the average number of portfolio committees per MP for a year using the following formula in cell Q2:

{% hint style="info" %}
\=AVERAGEIFS(P:P, E:E, E2)
{% endhint %}

Where:

* Column E = **year**
* Column P = **unique\_committee\_count\_per\_member\_for\_year**

We drag this formula down Column Q, and label it <mark style="color:red;">**average\_unique\_committee\_count\_per\_member\_for\_year**</mark>.

## <mark style="color:red;">STEP 10</mark> — Calculating a <mark style="color:red;">Parliamentary Attendance Rating (PAR)</mark> score per MP

Before we can calculate PAR scores, we have to adjust the **weighted\_attendance\_score** so that it accounts for the number of unique portfolio committees an MP subscribes to throughout a year. To do this, we use the following formula in cell R2:

{% hint style="info" %}
\=N2\*(1+(P2/Q2))
{% endhint %}

Where:

* Column N = **weighted\_attendance\_score**
* Column P = **unique\_committee\_count\_per\_member\_for\_year**
* Column Q = **average\_unique\_committee\_count\_per\_member\_for\_year**

We drag this formula down Column R, and label it <mark style="color:red;">**score\_adjusted\_for\_committees\_per\_member\_for\_year**</mark>.

Next, we want normalise the **score\_adjusted\_for\_committees\_per\_member\_for\_year** to a value of one (1), using the maximum value, for each year, from Column R. Assuming we a header row, we use the following formulae in cell S2:

{% hint style="info" %}
\=MAXIFS(R:R, E:E, E2)
{% endhint %}

Where:

* Column E = **year**
* Column R = **score\_adjusted\_for\_committees\_per\_member\_for\_year**

We drag this formula down Column S, and label it <mark style="color:red;">**max\_for\_year**</mark>. We can now normalise the values in Column R (**score\_adjusted\_for\_committees\_per\_member\_for\_year**) using the following formula in cell T2:

{% hint style="info" %}
\=R2/S2
{% endhint %}

Where:

* Column R = **score\_adjusted\_for\_committees\_per\_member\_for\_year**
* Column S = **max\_for\_year**

We drag this formula down Column T, and label it <mark style="color:red;">**par\_rating\_for\_year**</mark>.

We now have a <mark style="color:red;">**Parliamentary Attendance Rating (PAR) for each MP**</mark>, which takes into account their attendance across all portfolio committee meetings, and the number of unique portfolio committees they are subscribed to, through a given year.
