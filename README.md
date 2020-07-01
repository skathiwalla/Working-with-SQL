
/* Query 1 - top 25 spenders*/
SELECT   c.FirstName, c.Lastname, SUM(i.total) AS Money_Spent
FROM Invoice i
JOIN customer c
ON c.customerid=i.customerid
GROUP BY c.FirstName, c.Lastname
ORDER BY SUM(i.total) desc
LIMIT 25;

/* Query 2- top 25 Rock artists by number of songs*/
SELECT art.artistid, art.name, COUNT(g.name) AS Songs
FROM genre g
JOIN track t
ON g.genreid=t.genreid
JOIN album al
ON t.albumid=al.albumid
JOIN artist Art
ON al.artistid=art.artistid
WHERE g.name='Rock'
GROUP BY art.artistid, art.name
ORDER BY COUNT(g.name) DESC
LIMIT 25;

/*Query 3- top ten earning artists */
SELECT art.name, (SUM(il.quantity)*(il.unitprice)) as AMT_Spent
FROM InvoiceLine IL
JOIN Track T
ON IL.TRACKID=T.TRACKID
JOIN Album AL
ON t.albumid=AL.albumid
JOIN artist Art
ON al.artistid=art.artistid
GROUP BY art.name
ORDER BY (SUM(il.quantity)*(il.unitprice)) DESC
LIMIT 10;

/*Query 4- Top spenders for Iron Maiden */
SELECT c.customerid, c.firstname, c.lastname,
(SUM(inl.quantity)*inl.unitprice) AS Amt_spent
FROM Customer c
JOIN invoice inv
ON c.customerid=inv.customerid
JOIN invoiceline INL
ON inv.invoiceid=inl.invoiceid
JOIN track t
ON t.trackid=inl.trackid
JOIN Album Al
ON al.albumid=t.albumid
JOIN artist a
ON a.artistid=al.artistid
WHERE a.name='Iron Maiden'
GROUP BY 1,2,3
ORDER BY 4 DESC;
