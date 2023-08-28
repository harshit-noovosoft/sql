### Q1 : For our first foray into aggregates, we're going to stick to something simple. We want to know how many facilities exist - simply produce a total count.
![img.png](img.png)

### Q2 : Produce a count of the number of facilities that have a cost to guests of 10 or more.
![img_1.png](img_1.png)

### Q3 : Produce a count of the number of recommendations each member has made. Order by member ID.
![img_2.png](img_2.png)

### Q4 : Produce a list of the total number of slots booked per facility. For now, just produce an output table consisting of facility id and slots, sorted by facility id.
![img_3.png](img_3.png)

### Q5 : Produce a list of the total number of slots booked per facility in the month of September 2012. Produce an output table consisting of facility id and slots, sorted by the number of slots.
![img_4.png](img_4.png)

### Q6 : Produce a list of the total number of slots booked per facility per month in the year of 2012. Produce an output table consisting of facility id and slots, sorted by the id and month.
![img_5.png](img_5.png)

### Q7 : Find the total number of members (including guests) who have made at least one booking.
![img_6.png](img_6.png)

### Q8 : Produce a list of facilities with more than 1000 slots booked. Produce an output table consisting of facility id and slots, sorted by facility id.
![img_7.png](img_7.png)

### Q9 : Produce a list of facilities along with their total revenue. The output table should consist of facility name and revenue, sorted by revenue. Remember that there's a different cost for guests and members!
![img_8.png](img_8.png)

### Q10 : Produce a list of facilities with a total revenue less than 1000. Produce an output table consisting of facility name and revenue, sorted by revenue. Remember that there's a different cost for guests and members!
![img_9.png](img_9.png)

### Q11 : Output the facility id that has the highest number of slots booked. For bonus points, try a version without a LIMIT clause. This version will probably look messy!
![img_10.png](img_10.png)

### Q12 : Produce a list of the total number of slots booked per facility per month in the year of 2012. In this version, include output rows containing totals for all months per facility, and a total for all months for all facilities. The output table should consist of facility id, month and slots, sorted by the id and month. When calculating the aggregated values for all months and all facids, return null values in the month and facid columns.
![img_11.png](img_11.png)

### Q13 : Produce a list of the total number of hours booked per facility, remembering that a slot lasts half an hour. The output table should consist of the facility id, name, and hours booked, sorted by facility id. Try formatting the hours to two decimal places.
![img_12.png](img_12.png)

### Q14 : Produce a list of each member name, id, and their first booking after September 1st 2012. Order by member ID.
![img_13.png](img_13.png)

### Q15 : Produce a list of member names, with each row containing the total member count. Order by join date, and include guest members.
![img_14.png](img_14.png)

### Q16 : Produce a monotonically increasing numbered list of members (including guests), ordered by their date of joining. Remember that member IDs are not guaranteed to be sequential.
![img_15.png](img_15.png)

### Q17 : Output the facility id that has the highest number of slots booked. Ensure that in the event of a tie, all tieing results get output.
![img_16.png](img_16.png)

### Q18 : Produce a list of members (including guests), along with the number of hours they've booked in facilities, rounded to the nearest ten hours. Rank them by this rounded figure, producing output of first name, surname, rounded hours, rank. Sort by rank, surname, and first name.
![img_17.png](img_17.png)

### Q19 : Produce a list of the top three revenue generating facilities (including ties). Output facility name and rank, sorted by rank and facility name.
![img_18.png](img_18.png)

### Q20 : Classify facilities into equally sized groups of high, average, and low based on their revenue. Order by classification and facility name.
![img_19.png](img_19.png)

### Q21 : Based on the 3 complete months of data so far, calculate the amount of time each facility will take to repay its cost of ownership. Remember to take into account ongoing monthly maintenance. Output facility name and payback time in months, order by facility name. Don't worry about differences in month lengths, we're only looking for a rough value here!
![img_20.png](img_20.png)

### Q22 : For each day in August 2012, calculate a rolling average of total revenue over the previous 15 days. Output should contain date and revenue columns, sorted by the date. Remember to account for the possibility of a day having zero revenue. This one's a bit tough, so don't be afraid to check out the hint!
![img_21.png](img_21.png)
![img_22.png](img_22.png)