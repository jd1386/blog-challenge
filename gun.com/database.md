ram은 빠르다. rom보다 
file에 data를 저장하는건 memory를 쓰는 것보다 훨씬 느림
fs module은 업데이트를 할 수 없음. 쓰려면 처음부터 끝까지 다 써야함.
저녁먹기전가지만 mini sprint하기
node client 'mysql'이 있음 MYSQL에 있는 것을 가져와 쓸 수 있는것.
읽어보면서 따라하기
SQL은 평면적인 느낌이고, NOSQL은 입체적이어서 안으로 들어갈 수 있다. 표안에서 더 안으로 들어갈 수 있음.

메모리에 저장하는 것은 저장공간이 한정적이다. 용량이 작음

hashtable에서 중복될때, open addressing과 chaining 기억해두기 

node 환경에선 object가 생각보다 훨씬 복잡하게 구성되어 있다.

data를 저장할 때 stringify로 저장해놨다가 parse로 변환하면 좀더 효율적으로 할 수 있음

serialize- 입체를 평면화하는 느낌 stringify같은 것들

sql, nosql도 인덱스로 값을 찾는것은 O(1)이다.

프로젝트를 시작하기 전에 sql, nosql을 잡아야함

one to many 인경우가 있는데 그럴경우 누가 누구의 값을 가지고 있을지가 중요함. 예를 들어 교수와 수업의 경우

select는 read이다. 저장하는게 아님.



SQL에서 inner join과 outer join의 차이

Assuming you're joining on columns with no duplicates, which is a very common case:

- An inner join of A and B gives the result of A intersect B, i.e. the inner part of a [Venn diagram](http://en.wikipedia.org/wiki/Venn_diagram)intersection.
- An outer join of A and B gives the results of A union B, i.e. the outer parts of a Venn diagram union.

**Examples**

Suppose you have two tables, with a single column each, and data as follows:

```sql
A    B
-    -
1    3
2    4
3    5
4    6
```

Note that (1,2) are unique to A, (3,4) are common, and (5,6) are unique to B.

**Inner join**

An inner join using either of the equivalent queries gives the intersection of the two tables, i.e. the two rows they have in common.

```sql
select * from a INNER JOIN b on a.a = b.b;
select a.*, b.*  from a,b where a.a = b.b;

a | b
--+--
3 | 3
4 | 4
```

**Left outer join**

A left outer join will give all rows in A, plus any common rows in B.

```sql
select * from a LEFT OUTER JOIN b on a.a = b.b;
select a.*, b.*  from a,b where a.a = b.b(+);

a |  b
--+-----
1 | null
2 | null
3 |    3
4 |    4
```

**Right outer join**

A right outer join will give all rows in B, plus any common rows in A.

```sql
select * from a RIGHT OUTER JOIN b on a.a = b.b;
select a.*, b.*  from a,b where a.a(+) = b.b;

a    |  b
-----+----
3    |  3
4    |  4
null |  5
null |  6
```

**Full outer join**

A full outer join will give you the union of A and B, i.e. all the rows in A and all the rows in B. If something in A doesn't have a corresponding datum in B, then the B portion is null, and vice versa.

```sql
select * from a FULL OUTER JOIN b on a.a = b.b;

 a   |  b
-----+-----
   1 | null
   2 | null
   3 |    3
   4 |    4
null |    6
null |    5
```

update를 할때 예를 들어 id값을 1씩 증가시킨다면 1부터 적용하면 중복이 일어나므로 내림차순으로 실행해야한다.

### Logger는?

Morgan을 설명하기에 앞서 Logger가 무엇인지 알필요가 있다. Logger는 log의 데이터를 우리에게 보여준다 log는 IT인프라에서 발생하는 모든상황의 데이터를 담고있다. 예를들면 사용자가 브라우저에서 어떤url로 요청을 했을때 우리에게 사용자가 get방식 혹은post방식으로 요청했는지 언제 요청했는지 어디에서 요청했는지등의 정보를 우리에게 보여준다. Morgan은 Express프레임워크에서 사용할수 있는 logger이다. log기록을 통해 에러나 여러문제들이 어디에서 발생했는지등을 파악할수 있게 해준다.



### body-parser를 쓰는 이유

express에서는 req.body의 default값이 undefined로 지정되어있으므로, body-parser를 해서 값을 읽을 수 있게해줘야 한다.



### controller models router가 따로 있는 이유

결론적으로 역할을 나누고 크기를 줄여서 유지보수 재사용성 가독성을 높이기 위함임



callback을 넘겨줘서 받는 애는 사실 본인이 쓸 때 callback함수가 끝날 때까지 기다림. 비동기를 처리할 수 있음.



### sprint에서 실수한 부분

postman으로 요청을 보낼 때 header와 body를 같이 보내면 받을 때 body 만 걸러서 받아야 하는데 그럴 경우 npm test에 호환되지 못하고 일반적이지 못하다. 따라서 body만을 보내는 것이 훨씬 효율적이다.



#### LEFT JOIN 후에 INNER JOIN을 하면 NULL 값이 잘린다. 주의해야함!!!!!!!!

