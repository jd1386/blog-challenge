### express
- parsing 할 수 있게 도와줌
- 쿠키를 파싱할 수 있게 도와줌
- 세션을 유지?
- restful을 쉽게 도와줌

- app.post의 첫번재 인자로 라우팅을 해줌

.json(results)만 해도 알아서 잘 넘겨줌 -최근 원래는 send로 넘겨줬었음



onChange될 때마다 value에 state가 변경된 값을 다시 넘겨주는 경우가 있다. 

```java	
<input value={passwordValue} onChange={onPasswordChange} type="password"/>
```

위와 같은 경우인데 이를 inverting control in React 라고 하고 쓰는 예로는

욕설을 막는 기능을 구현하고 싶거나 키를 칠때마다 검색해서 사용자에게 보여주는 기능등을 구현하는 것이 있다.



### token의 장점

token의 장점은 보안이 아닌 서버의 확장성을 갖는 것이다. 세션이 존재할 때는 서버에 정보를 저장하고 일일이 정보를 확인한 후에 유저의 권한을 부여해야 하지만 token을 이용할 때는 token 자체에 권한이 담겨있기 때문에 서버에 정보를 저장할 필요가 없어 확장성이 좋다.

### jwt의 특징

jwt는 알고리즘방식이 들어있는 header와 정보가 들어있는 payload와 secret키가 담겨있는 signature로 구성된다.

jwt token 만들고 verify하는 예

```javascrip	
// 생성
const token = jwt.sign({
        email : req.body.email //첫번째 인자는 payload
      }, SECRET //두번째는 secret key, {expiresIn: 200} //마지막은 헤더로 사용할 수도 있고 만약에 입력을 안하면 sha256이 default이고 위와같이 시간적으면 유효시간 생성함);
// 확인
jwt.verify(token, SECRET, (err, decoded) => {
    if(err) throw err
    else{
        console.log(decoded.email)
    }
})
```



### how to send token in a cookie?

```java	
res.cookie('jwt',token); // add cookie here

#passport config
opts.jwtFromRequest = cookieExtractor; // check token in cookie
```



### sequelize

```java	
// 찾기
TABLE.findAll({
    where: {
        data: somedata
    }
})
// 생성
TABLE.create({
    where: {
        data: somedata
    }
})
```



**알아낸 사실: **

**남이 npm module을 install하고 내가 pull하더라도 다시 install해야함**

**res.send(JSON.stringify(something)) 와 res.json(something)은 같은 역할을 한다. **



encryption은 reverse가 가능하지만 hashing은 불가능함.

