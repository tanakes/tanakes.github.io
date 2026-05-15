[Link](https://pgexercises.com/questions/recursive/getdownward.html) to problem

![[Pasted image 20260515210911.png]]

```sql
with recursive cte as (
 	
  	select memid, firstname, surname, recommendedby from cd.members where recommendedby=1
  
	union all
	
  	select m.memid, m.firstname, m.surname, m.recommendedby from cd.members m 
  	join cte on m.recommendedby=cte.memid
)
select memid, firstname, surname from cte order by memid;
```

