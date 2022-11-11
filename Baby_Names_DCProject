## 1. Classic American names
<p>How have American baby name tastes changed since 1920?  Which names have remained popular for over 100 years, and how do those names compare to more recent top baby names? These are considerations for many new parents, but the skills we'll practice while answering these queries are broadly applicable. After all, understanding trends and popularity is important for many businesses, too! </p>
<p>We'll be working with data provided by the United States Social Security Administration, which lists first names along with the number and sex of babies they were given to in each year. For processing speed purposes, we've limited the dataset to first names which were given to over 5,000 American babies in a given year. Our data spans 101 years, from 1920 through 2020.</p>
<h3 id="baby_names"><code>baby_names</code></h3>
<table>
<thead>
<tr>
<th style="text-align:left;">column</th>
<th>type</th>
<th>meaning</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;"><code>year</code></td>
<td>int</td>
<td>year</td>
</tr>
<tr>
<td style="text-align:left;"><code>first_name</code></td>
<td>varchar</td>
<td>first name</td>
</tr>
<tr>
<td style="text-align:left;"><code>sex</code></td>
<td>varchar</td>
<td><code>sex</code> of babies given <code>first_name</code></td>
</tr>
<tr>
<td style="text-align:left;"><code>num</code></td>
<td>int</td>
<td>number of babies of <code>sex</code> given <code>first_name</code> in that <code>year</code></td>
</tr>
</tbody>
</table>
<p>Let's get oriented to American baby name tastes by looking at the names that have stood the test of time!</p>


```sql
%%sql
postgresql:///names
   
SELECT
    first_name,
    SUM(num) as sum
FROM baby_names
WHERE first_name IN
    /* Subquery to use only names that are on the chart all 101 years */
    (SELECT *
    FROM
        (SELECT first_name
        FROM baby_names
        GROUP BY first_name
        HAVING COUNT(year) = 101)
     AS timeless)
GROUP BY first_name
ORDER BY sum DESC;
```

    8 rows affected.





<table>
    <thead>
        <tr>
            <th>first_name</th>
            <th>sum</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>James</td>
            <td>4748138</td>
        </tr>
        <tr>
            <td>John</td>
            <td>4510721</td>
        </tr>
        <tr>
            <td>William</td>
            <td>3614424</td>
        </tr>
        <tr>
            <td>David</td>
            <td>3571498</td>
        </tr>
        <tr>
            <td>Joseph</td>
            <td>2361382</td>
        </tr>
        <tr>
            <td>Thomas</td>
            <td>2166802</td>
        </tr>
        <tr>
            <td>Charles</td>
            <td>2112352</td>
        </tr>
        <tr>
            <td>Elizabeth</td>
            <td>1436286</td>
        </tr>
    </tbody>
</table>





## 2. Timeless or trendy?
<p>Wow, it looks like there are a lot of timeless traditionally male names! Elizabeth is holding her own for the female names, too. </p>
<p>Now, let's broaden our understanding of the dataset by looking at all names. We'll attempt to capture the type of popularity that each name in the dataset enjoyed. Was the name classic and popular across many years or trendy, only popular for a few years? Let's find out. </p>


```sql
%%sql
postgresql:///names

SELECT
    first_name,
    SUM(num) AS sum,
    /* Sorting names into popularity types based on how many years they are on the list */
    CASE WHEN first_name IN
                (SELECT first_name
                FROM baby_names
                GROUP BY first_name
                HAVING COUNT(year) > 80)
            THEN 'Classic'
        WHEN first_name IN
                (SELECT first_name
                FROM baby_names
                GROUP BY first_name
                HAVING COUNT(year) > 50)
            THEN 'Semi-Classic'
        WHEN first_name IN
                (SELECT first_name
                FROM baby_names
                GROUP BY first_name
                HAVING COUNT(year) > 20)
            THEN 'Semi-trendy'
        ELSE 'Trendy'
        END AS popularity_type
FROM baby_names
GROUP BY first_name
ORDER BY first_name;
```

     * postgresql:///names
    547 rows affected.





<table>
    <thead>
        <tr>
            <th>first_name</th>
            <th>sum</th>
            <th>popularity_type</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Aaliyah</td>
            <td>15870</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Aaron</td>
            <td>530592</td>
            <td>Semi-Classic</td>
        </tr>
        <tr>
            <td>Abigail</td>
            <td>338485</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Adam</td>
            <td>497293</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Addison</td>
            <td>107433</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Adrian</td>
            <td>147741</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Aidan</td>
            <td>68566</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Aiden</td>
            <td>216194</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Alan</td>
            <td>162041</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Albert</td>
            <td>260945</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Alex</td>
            <td>158677</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Alexa</td>
            <td>33522</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Alexander</td>
            <td>579854</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Alexandra</td>
            <td>167122</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Alexandria</td>
            <td>5026</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Alexis</td>
            <td>282149</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Alfred</td>
            <td>16260</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Alice</td>
            <td>296559</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Alicia</td>
            <td>84579</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Allen</td>
            <td>10256</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Allison</td>
            <td>214995</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Alyssa</td>
            <td>269134</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Amanda</td>
            <td>699911</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Amber</td>
            <td>313418</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Amelia</td>
            <td>106381</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Amy</td>
            <td>569542</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Andrea</td>
            <td>321655</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Andrew</td>
            <td>1157548</td>
            <td>Semi-Classic</td>
        </tr>
        <tr>
            <td>Angel</td>
            <td>157667</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Angela</td>
            <td>541553</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Angelina</td>
            <td>11337</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Anita</td>
            <td>44692</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Ann</td>
            <td>336091</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Anna</td>
            <td>445496</td>
            <td>Semi-Classic</td>
        </tr>
        <tr>
            <td>Anne</td>
            <td>70228</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Annette</td>
            <td>49954</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Annie</td>
            <td>95837</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Anthony</td>
            <td>1344352</td>
            <td>Classic</td>
        </tr>
        <tr>
            <td>Antonio</td>
            <td>10097</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>April</td>
            <td>138714</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Aria</td>
            <td>52145</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Ariana</td>
            <td>5497</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Arianna</td>
            <td>5270</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Ariel</td>
            <td>5410</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Arthur</td>
            <td>309705</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Asher</td>
            <td>38156</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Ashley</td>
            <td>798738</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Ashton</td>
            <td>5436</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Aubrey</td>
            <td>72220</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Audrey</td>
            <td>48341</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Aurora</td>
            <td>5184</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Austin</td>
            <td>365295</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Ava</td>
            <td>265126</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Avery</td>
            <td>112293</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Ayden</td>
            <td>34244</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Bailey</td>
            <td>10219</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Barbara</td>
            <td>1343901</td>
            <td>Semi-Classic</td>
        </tr>
        <tr>
            <td>Barry</td>
            <td>85434</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Beatrice</td>
            <td>27983</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Bella</td>
            <td>5127</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Benjamin</td>
            <td>627696</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Bentley</td>
            <td>16844</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Bernice</td>
            <td>46347</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Beth</td>
            <td>55228</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Betty</td>
            <td>893396</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Beverly</td>
            <td>310683</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Billy</td>
            <td>270759</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Blake</td>
            <td>48795</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Bobby</td>
            <td>203289</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Bonnie</td>
            <td>193352</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Bradley</td>
            <td>147275</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Brandi</td>
            <td>16199</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Brandon</td>
            <td>729832</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Brandy</td>
            <td>48762</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Brayden</td>
            <td>93754</td>
            <td>Trendy</td>
        </tr>
        <tr>
            <td>Brenda</td>
            <td>513283</td>
            <td>Semi-trendy</td>
        </tr>
        <tr>
            <td>Brian</td>
            <td>1107302</td>
            <td>Semi-Classic</td>
        </tr>
   </tbody>
</table>



## 3. Top-ranked female names since 1920
<p>Did you find your favorite American celebrity's name on the popularity chart? Was it classic or trendy? How do you think the name Henry did? What about Jaxon?</p>
<p>Since we didn't get many traditionally female names in our classic American names search in the first task, let's limit our search to names which were given to female babies. </p>
<p>We can use this opportunity to practice window functions by assigning a rank to female names based on the number of babies that have ever been given that name. What are the top-ranked female names since 1920?</p>


```sql
%%sql

SELECT
    RANK() OVER (ORDER BY SUM(num) DESC) name_rank, -- Ranking by highest overall total of babies with that name
    first_name,
    SUM(num) as sum
FROM baby_names
WHERE sex = 'F'
GROUP BY first_name
LIMIT 10;
```

     * postgresql:///names
    10 rows affected.





<table>
    <thead>
        <tr>
            <th>name_rank</th>
            <th>first_name</th>
            <th>sum</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1</td>
            <td>Mary</td>
            <td>3215850</td>
        </tr>
        <tr>
            <td>2</td>
            <td>Patricia</td>
            <td>1479802</td>
        </tr>
        <tr>
            <td>3</td>
            <td>Elizabeth</td>
            <td>1436286</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Jennifer</td>
            <td>1404743</td>
        </tr>
        <tr>
            <td>5</td>
            <td>Linda</td>
            <td>1361021</td>
        </tr>
        <tr>
            <td>6</td>
            <td>Barbara</td>
            <td>1343901</td>
        </tr>
        <tr>
            <td>7</td>
            <td>Susan</td>
            <td>1025728</td>
        </tr>
        <tr>
            <td>8</td>
            <td>Jessica</td>
            <td>994210</td>
        </tr>
        <tr>
            <td>9</td>
            <td>Lisa</td>
            <td>920119</td>
        </tr>
        <tr>
            <td>10</td>
            <td>Betty</td>
            <td>893396</td>
        </tr>
    </tbody>
</table>





## 4. Picking a baby name
<p>Perhaps a friend has heard of our work analyzing baby names and would like help choosing a name for her baby, a girl. She doesn't like any of the top-ranked names we found in the previous task. </p>
<p>She's set on a traditionally female name ending in the letter 'a' since she's heard that vowels in baby names are trendy. She's also looking for a name that has been popular in the years since 2015. </p>
<p>Let's see what we can do to find some options for this friend!</p>


```sql
%%sql

SELECT
    first_name
FROM
    baby_names
WHERE
    sex = 'F' AND
    year > 2015 AND
    first_name LIKE '%a'
GROUP BY first_name
ORDER BY sum(num) DESC;
```

     * postgresql:///names
    19 rows affected.





<table>
    <thead>
        <tr>
            <th>first_name</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Olivia</td>
        </tr>
        <tr>
            <td>Emma</td>
        </tr>
        <tr>
            <td>Ava</td>
        </tr>
        <tr>
            <td>Sophia</td>
        </tr>
        <tr>
            <td>Isabella</td>
        </tr>
        <tr>
            <td>Mia</td>
        </tr>
        <tr>
            <td>Amelia</td>
        </tr>
        <tr>
            <td>Ella</td>
        </tr>
        <tr>
            <td>Sofia</td>
        </tr>
        <tr>
            <td>Camila</td>
        </tr>
        <tr>
            <td>Aria</td>
        </tr>
        <tr>
            <td>Victoria</td>
        </tr>
        <tr>
            <td>Layla</td>
        </tr>
        <tr>
            <td>Nora</td>
        </tr>
        <tr>
            <td>Mila</td>
        </tr>
        <tr>
            <td>Luna</td>
        </tr>
        <tr>
            <td>Stella</td>
        </tr>
        <tr>
            <td>Gianna</td>
        </tr>
        <tr>
            <td>Aurora</td>
        </tr>
    </tbody>
</table>




## 5. The Olivia expansion
<p>Based on the results in the previous task, we can see that Olivia is the most popular female name ending in 'A' since 2015. When did the name Olivia become so popular?</p>
<p>Let's explore the rise of the name Olivia with the help of a window function.</p>


```sql
%%sql

SELECT
    year,
    first_name,
    num,
    /* Running total of babies named Olivia */
    SUM(num) OVER
        (ORDER BY year)
        AS cumulative_olivias
FROM
    baby_names
WHERE first_name = 'Olivia'
ORDER BY year;
```

     * postgresql:///names
    30 rows affected.





<table>
    <thead>
        <tr>
            <th>year</th>
            <th>first_name</th>
            <th>num</th>
            <th>cumulative_olivias</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1991</td>
            <td>Olivia</td>
            <td>5601</td>
            <td>5601</td>
        </tr>
        <tr>
            <td>1992</td>
            <td>Olivia</td>
            <td>5809</td>
            <td>11410</td>
        </tr>
        <tr>
            <td>1993</td>
            <td>Olivia</td>
            <td>6340</td>
            <td>17750</td>
        </tr>
        <tr>
            <td>1994</td>
            <td>Olivia</td>
            <td>6434</td>
            <td>24184</td>
        </tr>
        <tr>
            <td>1995</td>
            <td>Olivia</td>
            <td>7624</td>
            <td>31808</td>
        </tr>
        <tr>
            <td>1996</td>
            <td>Olivia</td>
            <td>8124</td>
            <td>39932</td>
        </tr>
        <tr>
            <td>1997</td>
            <td>Olivia</td>
            <td>9477</td>
            <td>49409</td>
        </tr>
        <tr>
            <td>1998</td>
            <td>Olivia</td>
            <td>10610</td>
            <td>60019</td>
        </tr>
        <tr>
            <td>1999</td>
            <td>Olivia</td>
            <td>11255</td>
            <td>71274</td>
        </tr>
        <tr>
            <td>2000</td>
            <td>Olivia</td>
            <td>12852</td>
            <td>84126</td>
        </tr>
        <tr>
            <td>2001</td>
            <td>Olivia</td>
            <td>13977</td>
            <td>98103</td>
        </tr>
        <tr>
            <td>2002</td>
            <td>Olivia</td>
            <td>14630</td>
            <td>112733</td>
        </tr>
        <tr>
            <td>2003</td>
            <td>Olivia</td>
            <td>16152</td>
            <td>128885</td>
        </tr>
        <tr>
            <td>2004</td>
            <td>Olivia</td>
            <td>16106</td>
            <td>144991</td>
        </tr>
        <tr>
            <td>2005</td>
            <td>Olivia</td>
            <td>15694</td>
            <td>160685</td>
        </tr>
        <tr>
            <td>2006</td>
            <td>Olivia</td>
            <td>15501</td>
            <td>176186</td>
        </tr>
        <tr>
            <td>2007</td>
            <td>Olivia</td>
            <td>16584</td>
            <td>192770</td>
        </tr>
        <tr>
            <td>2008</td>
            <td>Olivia</td>
            <td>17084</td>
            <td>209854</td>
        </tr>
        <tr>
            <td>2009</td>
            <td>Olivia</td>
            <td>17438</td>
            <td>227292</td>
        </tr>
        <tr>
            <td>2010</td>
            <td>Olivia</td>
            <td>17029</td>
            <td>244321</td>
        </tr>
        <tr>
            <td>2011</td>
            <td>Olivia</td>
            <td>17327</td>
            <td>261648</td>
        </tr>
        <tr>
            <td>2012</td>
            <td>Olivia</td>
            <td>17320</td>
            <td>278968</td>
        </tr>
        <tr>
            <td>2013</td>
            <td>Olivia</td>
            <td>18439</td>
            <td>297407</td>
        </tr>
        <tr>
            <td>2014</td>
            <td>Olivia</td>
            <td>19823</td>
            <td>317230</td>
        </tr>
        <tr>
            <td>2015</td>
            <td>Olivia</td>
            <td>19710</td>
            <td>336940</td>
        </tr>
        <tr>
            <td>2016</td>
            <td>Olivia</td>
            <td>19380</td>
            <td>356320</td>
        </tr>
        <tr>
            <td>2017</td>
            <td>Olivia</td>
            <td>18744</td>
            <td>375064</td>
        </tr>
        <tr>
            <td>2018</td>
            <td>Olivia</td>
            <td>18011</td>
            <td>393075</td>
        </tr>
        <tr>
            <td>2019</td>
            <td>Olivia</td>
            <td>18508</td>
            <td>411583</td>
        </tr>
        <tr>
            <td>2020</td>
            <td>Olivia</td>
            <td>17535</td>
            <td>429118</td>
        </tr>
    </tbody>
</table>






## 6. Many males with the same name
<p>Wow, Olivia has had a meteoric rise! Let's take a look at traditionally male names now. We saw in the first task that there are nine traditionally male names given to at least 5,000 babies every single year in our 101-year dataset! Those names are classics, but showing up in the dataset every year doesn't necessarily mean that the timeless names were the most popular. Let's explore popular male names a little further.</p>
<p>In the next two tasks, we will build up to listing every year along with the most popular male name in that year. This presents a common problem: how do we find the greatest X in a group? Or, in the context of this problem, how do we find the male name given to the highest number of babies in a year? </p>
<p>In SQL, one approach is to use a subquery. We can first write a query that selects the <code>year</code> and the maximum <code>num</code> of babies given any single male name in that year. For example, in 1989, the male name given to the highest number of babies was given to 65,339 babies. We'll write this query in this task. In the next task, we can use the code from this task as a subquery to look up the <code>first_name</code> that was given to 65,339 babies in 1989… as well as the top male first name for all other years!</p>


```sql
%%sql


SELECT
    year,
    MAX(num) as max_num
FROM baby_names
WHERE sex = 'M'
GROUP BY year;
```

     * postgresql:///names
    101 rows affected.





<table>
    <thead>
        <tr>
            <th>year</th>
            <th>max_num</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1970</td>
            <td>85291</td>
        </tr>
        <tr>
            <td>2000</td>
            <td>34483</td>
        </tr>
        <tr>
            <td>1947</td>
            <td>94764</td>
        </tr>
        <tr>
            <td>1962</td>
            <td>85041</td>
        </tr>
        <tr>
            <td>1975</td>
            <td>68451</td>
        </tr>
        <tr>
            <td>1980</td>
            <td>68704</td>
        </tr>
        <tr>
            <td>1931</td>
            <td>60518</td>
        </tr>
        <tr>
            <td>1981</td>
            <td>68776</td>
        </tr>
        <tr>
            <td>2013</td>
            <td>18266</td>
        </tr>
        <tr>
            <td>1972</td>
            <td>71401</td>
        </tr>
        <tr>
            <td>1956</td>
            <td>90665</td>
        </tr>
        <tr>
            <td>2007</td>
            <td>24292</td>
        </tr>
        <tr>
            <td>1948</td>
            <td>88589</td>
        </tr>
        <tr>
            <td>1984</td>
            <td>67745</td>
        </tr>
        <tr>
            <td>1957</td>
            <td>92718</td>
        </tr>
        <tr>
            <td>1961</td>
            <td>86917</td>
        </tr>
        <tr>
            <td>2002</td>
            <td>30579</td>
        </tr>
        <tr>
            <td>1925</td>
            <td>60897</td>
        </tr>
        <tr>
            <td>1992</td>
            <td>54397</td>
        </tr>
        <tr>
            <td>2008</td>
            <td>22603</td>
        </tr>
        <tr>
            <td>1958</td>
            <td>90564</td>
        </tr>
        <tr>
            <td>1971</td>
            <td>77599</td>
        </tr>
        <tr>
            <td>1985</td>
            <td>64924</td>
        </tr>
        <tr>
            <td>1926</td>
            <td>61130</td>
        </tr>
        <tr>
            <td>1988</td>
            <td>64150</td>
        </tr>
        <tr>
            <td>1929</td>
            <td>59804</td>
        </tr>
        <tr>
            <td>1963</td>
            <td>83778</td>
        </tr>
        <tr>
            <td>1928</td>
            <td>60703</td>
        </tr>
        <tr>
            <td>2003</td>
            <td>29643</td>
        </tr>
        <tr>
            <td>1930</td>
            <td>62149</td>
        </tr>
        <tr>
            <td>1951</td>
            <td>87261</td>
        </tr>
        <tr>
            <td>1940</td>
            <td>62476</td>
        </tr>
        <tr>
            <td>1982</td>
            <td>68244</td>
        </tr>
        <tr>
            <td>1920</td>
            <td>56914</td>
        </tr>
        <tr>
            <td>1999</td>
            <td>35367</td>
        </tr>
        <tr>
            <td>1952</td>
            <td>87063</td>
        </tr>
        <tr>
            <td>2020</td>
            <td>19659</td>
        </tr>
        <tr>
            <td>1946</td>
            <td>87439</td>
        </tr>
        <tr>
            <td>1968</td>
            <td>81995</td>
        </tr>
        <tr>
            <td>1996</td>
            <td>38365</td>
        </tr>
        <tr>
            <td>2005</td>
            <td>25837</td>
        </tr>
        <tr>
            <td>1923</td>
            <td>57469</td>
        </tr>
        <tr>
            <td>2009</td>
            <td>21184</td>
        </tr>
        <tr>
            <td>1924</td>
            <td>60801</td>
        </tr>
        <tr>
            <td>1954</td>
            <td>88576</td>
        </tr>
        <tr>
            <td>2004</td>
            <td>27886</td>
        </tr>
        <tr>
            <td>1938</td>
            <td>62269</td>
        </tr>
        <tr>
            <td>1942</td>
            <td>77174</td>
        </tr>
        <tr>
            <td>1966</td>
            <td>79990</td>
        </tr>
        <tr>
            <td>1998</td>
            <td>36616</td>
        </tr>
        <tr>
            <td>1974</td>
            <td>67580</td>
        </tr>
        <tr>
            <td>1949</td>
            <td>86865</td>
        </tr>
        <tr>
            <td>1990</td>
            <td>65302</td>
        </tr>
        <tr>
            <td>1995</td>
            <td>41399</td>
        </tr>
        <tr>
            <td>1973</td>
            <td>67842</td>
        </tr>
        <tr>
            <td>1927</td>
            <td>61671</td>
        </tr>
        <tr>
            <td>1941</td>
            <td>66743</td>
        </tr>
        <tr>
            <td>1977</td>
            <td>67609</td>
        </tr>
        <tr>
            <td>2001</td>
            <td>32554</td>
        </tr>
        <tr>
            <td>1997</td>
            <td>37549</td>
        </tr>
        <tr>
            <td>2014</td>
            <td>19319</td>
        </tr>
        <tr>
            <td>1965</td>
            <td>81021</td>
        </tr>
        <tr>
            <td>1935</td>
            <td>56522</td>
        </tr>
        <tr>
            <td>1944</td>
            <td>76954</td>
        </tr>
        <tr>
            <td>1994</td>
            <td>44472</td>
        </tr>
        <tr>
            <td>2016</td>
            <td>19154</td>
        </tr>
        <tr>
            <td>1960</td>
            <td>85933</td>
        </tr>
        <tr>
            <td>1987</td>
            <td>63654</td>
        </tr>
        <tr>
            <td>1978</td>
            <td>67157</td>
        </tr>
        <tr>
            <td>2018</td>
            <td>19924</td>
        </tr>
        <tr>
            <td>2006</td>
            <td>24850</td>
        </tr>
        <tr>
            <td>1921</td>
            <td>58215</td>
        </tr>
        <tr>
            <td>1993</td>
            <td>49554</td>
        </tr>
        <tr>
            <td>1964</td>
            <td>82642</td>
        </tr>
        <tr>
            <td>1943</td>
            <td>80274</td>
        </tr>
        <tr>
            <td>1937</td>
            <td>61842</td>
        </tr>
        <tr>
            <td>1986</td>
            <td>64224</td>
        </tr>
        <tr>
            <td>1953</td>
            <td>86247</td>
        </tr>
        <tr>
            <td>1959</td>
            <td>85224</td>
        </tr>
        <tr>
            <td>1976</td>
            <td>66947</td>
        </tr>
        <tr>
            <td>1989</td>
            <td>65399</td>
        </tr>
        <tr>
            <td>2012</td>
            <td>19088</td>
        </tr>
        <tr>
            <td>2011</td>
            <td>20378</td>
        </tr>
        <tr>
            <td>2019</td>
            <td>20555</td>
        </tr>
        <tr>
            <td>1955</td>
            <td>88372</td>
        </tr>
        <tr>
            <td>1939</td>
            <td>59653</td>
        </tr>
        <tr>
            <td>1979</td>
            <td>67742</td>
        </tr>
        <tr>
            <td>1991</td>
            <td>60793</td>
        </tr>
        <tr>
            <td>2017</td>
            <td>18824</td>
        </tr>
        <tr>
            <td>1969</td>
            <td>85201</td>
        </tr>
        <tr>
            <td>2015</td>
            <td>19650</td>
        </tr>
        <tr>
            <td>2010</td>
            <td>22139</td>
        </tr>
        <tr>
            <td>1932</td>
            <td>59265</td>
        </tr>
        <tr>
            <td>1967</td>
            <td>82440</td>
        </tr>
        <tr>
            <td>1922</td>
            <td>57280</td>
        </tr>
        <tr>
            <td>1933</td>
            <td>54223</td>
        </tr>
        <tr>
            <td>1934</td>
            <td>55834</td>
        </tr>
        <tr>
            <td>1936</td>
            <td>58499</td>
        </tr>
        <tr>
            <td>1945</td>
            <td>74460</td>
        </tr>
        <tr>
            <td>1950</td>
            <td>86229</td>
        </tr>
        <tr>
            <td>1983</td>
            <td>68010</td>
        </tr>
    </tbody>
</table>







## 7. Top male names over the years
<p>In the previous task, we found the maximum number of babies given any one male name in each year. Incredibly, the most popular name each year varied from being given to less than 20,000 babies to being given to more than 90,000! </p>
<p>In this task, we find out what that top male name is for each year in our dataset. </p>


```sql
%%sql


SELECT
    b.year,
    b.first_name,
    b.num
FROM baby_names as b
    JOIN (
        SELECT
            year,
            MAX(num) as max_num
        FROM baby_names
        WHERE sex = 'M'
        GROUP BY year)
        AS sub
    /* Only names whose number match the MAXIMUM number for that year */
    ON b.year = sub.year AND b.num = sub.max_num
ORDER BY year DESC;
```

     * postgresql:///names
    101 rows affected.





<table>
    <thead>
        <tr>
            <th>year</th>
            <th>first_name</th>
            <th>num</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>2020</td>
            <td>Liam</td>
            <td>19659</td>
        </tr>
        <tr>
            <td>2019</td>
            <td>Liam</td>
            <td>20555</td>
        </tr>
        <tr>
            <td>2018</td>
            <td>Liam</td>
            <td>19924</td>
        </tr>
        <tr>
            <td>2017</td>
            <td>Liam</td>
            <td>18824</td>
        </tr>
        <tr>
            <td>2016</td>
            <td>Noah</td>
            <td>19154</td>
        </tr>
        <tr>
            <td>2015</td>
            <td>Noah</td>
            <td>19650</td>
        </tr>
        <tr>
            <td>2014</td>
            <td>Noah</td>
            <td>19319</td>
        </tr>
        <tr>
            <td>2013</td>
            <td>Noah</td>
            <td>18266</td>
        </tr>
        <tr>
            <td>2012</td>
            <td>Jacob</td>
            <td>19088</td>
        </tr>
        <tr>
            <td>2011</td>
            <td>Jacob</td>
            <td>20378</td>
        </tr>
        <tr>
            <td>2010</td>
            <td>Jacob</td>
            <td>22139</td>
        </tr>
        <tr>
            <td>2009</td>
            <td>Jacob</td>
            <td>21184</td>
        </tr>
        <tr>
            <td>2008</td>
            <td>Jacob</td>
            <td>22603</td>
        </tr>
        <tr>
            <td>2007</td>
            <td>Jacob</td>
            <td>24292</td>
        </tr>
        <tr>
            <td>2006</td>
            <td>Jacob</td>
            <td>24850</td>
        </tr>
        <tr>
            <td>2005</td>
            <td>Jacob</td>
            <td>25837</td>
        </tr>
        <tr>
            <td>2004</td>
            <td>Jacob</td>
            <td>27886</td>
        </tr>
        <tr>
            <td>2003</td>
            <td>Jacob</td>
            <td>29643</td>
        </tr>
        <tr>
            <td>2002</td>
            <td>Jacob</td>
            <td>30579</td>
        </tr>
        <tr>
            <td>2001</td>
            <td>Jacob</td>
            <td>32554</td>
        </tr>
        <tr>
            <td>2000</td>
            <td>Jacob</td>
            <td>34483</td>
        </tr>
        <tr>
            <td>1999</td>
            <td>Jacob</td>
            <td>35367</td>
        </tr>
        <tr>
            <td>1998</td>
            <td>Michael</td>
            <td>36616</td>
        </tr>
        <tr>
            <td>1997</td>
            <td>Michael</td>
            <td>37549</td>
        </tr>
        <tr>
            <td>1996</td>
            <td>Michael</td>
            <td>38365</td>
        </tr>
        <tr>
            <td>1995</td>
            <td>Michael</td>
            <td>41399</td>
        </tr>
        <tr>
            <td>1994</td>
            <td>Michael</td>
            <td>44472</td>
        </tr>
        <tr>
            <td>1993</td>
            <td>Michael</td>
            <td>49554</td>
        </tr>
        <tr>
            <td>1992</td>
            <td>Michael</td>
            <td>54397</td>
        </tr>
        <tr>
            <td>1991</td>
            <td>Michael</td>
            <td>60793</td>
        </tr>
        <tr>
            <td>1990</td>
            <td>Michael</td>
            <td>65302</td>
        </tr>
        <tr>
            <td>1989</td>
            <td>Michael</td>
            <td>65399</td>
        </tr>
        <tr>
            <td>1988</td>
            <td>Michael</td>
            <td>64150</td>
        </tr>
        <tr>
            <td>1987</td>
            <td>Michael</td>
            <td>63654</td>
        </tr>
        <tr>
            <td>1986</td>
            <td>Michael</td>
            <td>64224</td>
        </tr>
        <tr>
            <td>1985</td>
            <td>Michael</td>
            <td>64924</td>
        </tr>
        <tr>
            <td>1984</td>
            <td>Michael</td>
            <td>67745</td>
        </tr>
        <tr>
            <td>1983</td>
            <td>Michael</td>
            <td>68010</td>
        </tr>
        <tr>
            <td>1982</td>
            <td>Michael</td>
            <td>68244</td>
        </tr>
        <tr>
            <td>1981</td>
            <td>Michael</td>
            <td>68776</td>
        </tr>
        <tr>
            <td>1980</td>
            <td>Michael</td>
            <td>68704</td>
        </tr>
        <tr>
            <td>1979</td>
            <td>Michael</td>
            <td>67742</td>
        </tr>
        <tr>
            <td>1978</td>
            <td>Michael</td>
            <td>67157</td>
        </tr>
        <tr>
            <td>1977</td>
            <td>Michael</td>
            <td>67609</td>
        </tr>
        <tr>
            <td>1976</td>
            <td>Michael</td>
            <td>66947</td>
        </tr>
        <tr>
            <td>1975</td>
            <td>Michael</td>
            <td>68451</td>
        </tr>
        <tr>
            <td>1974</td>
            <td>Michael</td>
            <td>67580</td>
        </tr>
        <tr>
            <td>1973</td>
            <td>Michael</td>
            <td>67842</td>
        </tr>
        <tr>
            <td>1972</td>
            <td>Michael</td>
            <td>71401</td>
        </tr>
        <tr>
            <td>1971</td>
            <td>Michael</td>
            <td>77599</td>
        </tr>
        <tr>
            <td>1970</td>
            <td>Michael</td>
            <td>85291</td>
        </tr>
        <tr>
            <td>1969</td>
            <td>Michael</td>
            <td>85201</td>
        </tr>
        <tr>
            <td>1968</td>
            <td>Michael</td>
            <td>81995</td>
        </tr>
        <tr>
            <td>1967</td>
            <td>Michael</td>
            <td>82440</td>
        </tr>
        <tr>
            <td>1966</td>
            <td>Michael</td>
            <td>79990</td>
        </tr>
        <tr>
            <td>1965</td>
            <td>Michael</td>
            <td>81021</td>
        </tr>
        <tr>
            <td>1964</td>
            <td>Michael</td>
            <td>82642</td>
        </tr>
        <tr>
            <td>1963</td>
            <td>Michael</td>
            <td>83778</td>
        </tr>
        <tr>
            <td>1962</td>
            <td>Michael</td>
            <td>85041</td>
        </tr>
        <tr>
            <td>1961</td>
            <td>Michael</td>
            <td>86917</td>
        </tr>
        <tr>
            <td>1960</td>
            <td>David</td>
            <td>85933</td>
        </tr>
        <tr>
            <td>1959</td>
            <td>Michael</td>
            <td>85224</td>
        </tr>
        <tr>
            <td>1958</td>
            <td>Michael</td>
            <td>90564</td>
        </tr>
        <tr>
            <td>1957</td>
            <td>Michael</td>
            <td>92718</td>
        </tr>
        <tr>
            <td>1956</td>
            <td>Michael</td>
            <td>90665</td>
        </tr>
        <tr>
            <td>1955</td>
            <td>Michael</td>
            <td>88372</td>
        </tr>
        <tr>
            <td>1954</td>
            <td>Michael</td>
            <td>88576</td>
        </tr>
        <tr>
            <td>1953</td>
            <td>Robert</td>
            <td>86247</td>
        </tr>
        <tr>
            <td>1952</td>
            <td>James</td>
            <td>87063</td>
        </tr>
        <tr>
            <td>1951</td>
            <td>James</td>
            <td>87261</td>
        </tr>
        <tr>
            <td>1950</td>
            <td>James</td>
            <td>86229</td>
        </tr>
        <tr>
            <td>1949</td>
            <td>James</td>
            <td>86865</td>
        </tr>
        <tr>
            <td>1948</td>
            <td>James</td>
            <td>88589</td>
        </tr>
        <tr>
            <td>1947</td>
            <td>James</td>
            <td>94764</td>
        </tr>
        <tr>
            <td>1946</td>
            <td>James</td>
            <td>87439</td>
        </tr>
        <tr>
            <td>1945</td>
            <td>James</td>
            <td>74460</td>
        </tr>
        <tr>
            <td>1944</td>
            <td>James</td>
            <td>76954</td>
        </tr>
        <tr>
            <td>1943</td>
            <td>James</td>
            <td>80274</td>
        </tr>
        <tr>
            <td>1942</td>
            <td>James</td>
            <td>77174</td>
        </tr>
        <tr>
            <td>1941</td>
            <td>James</td>
            <td>66743</td>
        </tr>
        <tr>
            <td>1940</td>
            <td>James</td>
            <td>62476</td>
        </tr>
        <tr>
            <td>1939</td>
            <td>Robert</td>
            <td>59653</td>
        </tr>
        <tr>
            <td>1938</td>
            <td>Robert</td>
            <td>62269</td>
        </tr>
        <tr>
            <td>1937</td>
            <td>Robert</td>
            <td>61842</td>
        </tr>
        <tr>
            <td>1936</td>
            <td>Robert</td>
            <td>58499</td>
        </tr>
        <tr>
            <td>1935</td>
            <td>Robert</td>
            <td>56522</td>
        </tr>
        <tr>
            <td>1934</td>
            <td>Robert</td>
            <td>55834</td>
        </tr>
        <tr>
            <td>1933</td>
            <td>Robert</td>
            <td>54223</td>
        </tr>
        <tr>
            <td>1932</td>
            <td>Robert</td>
            <td>59265</td>
        </tr>
        <tr>
            <td>1931</td>
            <td>Robert</td>
            <td>60518</td>
        </tr>
        <tr>
            <td>1930</td>
            <td>Robert</td>
            <td>62149</td>
        </tr>
        <tr>
            <td>1929</td>
            <td>Robert</td>
            <td>59804</td>
        </tr>
        <tr>
            <td>1928</td>
            <td>Robert</td>
            <td>60703</td>
        </tr>
        <tr>
            <td>1927</td>
            <td>Robert</td>
            <td>61671</td>
        </tr>
        <tr>
            <td>1926</td>
            <td>Robert</td>
            <td>61130</td>
        </tr>
        <tr>
            <td>1925</td>
            <td>Robert</td>
            <td>60897</td>
        </tr>
        <tr>
            <td>1924</td>
            <td>Robert</td>
            <td>60801</td>
        </tr>
        <tr>
            <td>1923</td>
            <td>John</td>
            <td>57469</td>
        </tr>
        <tr>
            <td>1922</td>
            <td>John</td>
            <td>57280</td>
        </tr>
        <tr>
            <td>1921</td>
            <td>John</td>
            <td>58215</td>
        </tr>
        <tr>
            <td>1920</td>
            <td>John</td>
            <td>56914</td>
        </tr>
    </tbody>
</table>




## 8. The most years at number one
<p>Noah and Liam have ruled the roost in the last few years, but if we scroll down in the results, it looks like Michael and Jacob have also spent a good number of years as the top name! Which name has been number one for the largest number of years? Let's use a common table expression to find out. </p>


```sql
%%sql


WITH top_male_names AS 
    (SELECT
        b.year,
        b.first_name,
        b.num
    FROM baby_names as b
        JOIN (
            SELECT
                year,
                MAX(num) as max_num
            FROM baby_names
            WHERE sex = 'M'
            GROUP BY year)
            AS sub
        ON b.year = sub.year AND b.num = sub.max_num
    ORDER BY year DESC
    )
SELECT
    first_name,
    COUNT(*) as count_top_name
FROM
    top_male_names
GROUP BY first_name
ORDER BY count_top_name DESC;
```

     * postgresql:///names
    8 rows affected.





<table>
    <thead>
        <tr>
            <th>first_name</th>
            <th>count_top_name</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Michael</td>
            <td>44</td>
        </tr>
        <tr>
            <td>Robert</td>
            <td>17</td>
        </tr>
        <tr>
            <td>Jacob</td>
            <td>14</td>
        </tr>
        <tr>
            <td>James</td>
            <td>13</td>
        </tr>
        <tr>
            <td>Noah</td>
            <td>4</td>
        </tr>
        <tr>
            <td>John</td>
            <td>4</td>
        </tr>
        <tr>
            <td>Liam</td>
            <td>4</td>
        </tr>
        <tr>
            <td>David</td>
            <td>1</td>
        </tr>
    </tbody>
</table>
