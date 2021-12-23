# Promise(async in javascript)

정해진 장시간의 기능을 수행하고 나서 정상적으로 처리되었다면 메세지와 함께 값을 전달해주고,
정상적으로 처리되지 않았다면 에러를 전달해줌.

### 상태(state) : pending(기능이 수행중인 상태) -> fulfilled(기능이 완료된 상태) or rejected(기능이 실패)

### producer(정보 제공) vs consumer(정보 소비)



## Producer

````javascript
// 1. Producer
// 프로미스가 생성될때 executor라는 콜백함수가 자동으로 실행됨.
const promise = new Promise((resolve, reject)=> {
  // doing some heavy work (network, reading files)
  console.log('doing something...'); // executor 콜바로 실행되는 것을 확인할 수 있음.
  setTimeout(() => {
    // resolve('결과'); // resolve로 결과를 전s달
    reject(new Error('no network')) 
  }, 2000);
});
````



## Consumers

```javascript

// 2.Consumer: then, catch, finally
promise
  .then((value)=> { // resolve에서 전달해준 값이 매개변수로 들어감
    console.log(value); 
  })
  .catch(error => { // reject에서 전달해준 에러가 매개변수로 들어감
    console.log(error)
  })
  .finally(()=> { // promise가 성공하든 실패하든 실행됨.
    console.log('finally')
  })

```



## Promise Chaining

```JavaScript
// 3. Promise chaining
const fetchNumber = new Promise((resolve, reject)=> {
  setTimeout(() => resolve(1), 1000);
})

fetchNumber
  .then(num => num * 2)
  .then(num => num * 3)
  .then(num => {
    return new Promise((resolve, reject)=> {
      setTimeout(() => resolve(num - 1), 1000);
    });
  })
  .then(num => console.log(num));
```



## Promise Chaining Error Handling

```JavaScript
// 4. Promise Chaining Error Handling
const getHen = () => 
  new Promise((resolve, reject) => {
    setTimeout(() => resolve('🐓'), 1000)
  });
const getEgg = hen => 
  new Promise((resolve, reject) => {
    // setTimeout(() => resolve(`${hen} => 🥚`), 1000)
    setTimeout(() => reject(new Error(`error! ${hen} => 🥚`)), 1000)
  })
const cook = egg => 
  new Promise((resolve, reject) => {
    setTimeout(()=> resolve(`${egg} => 🍳`), 1000)
  })

getHen()
  .then(getEgg) //.then(hen => getEgg(hen)) 전달하는 값을 갯수와 함수가 받는 매개변수의 갯수가 같으면 매개변수를 전달하는 것을 생략하여 적을 수 있음
  .catch(error => { // 바로 다음에 catch를 사용해서 단께별로 에러를 처리할 수 있음     
    return '🥖'
  })
  .then(cook) //.then(egg => cook(egg))
  .then(console.log) //.then(meal => console.log(meal))
  .catch(console.log)
```



## Callback Hell to Promise

```JavaScript
class UserStorage {
  loginUser(id, password) {
    return new Promise((resolve, reject) => {
      setTimeout(()=> {
        if (
          (id=='cho' && password=='1234') || 
          (id=='kim' && password=='2580')
        ) {
          resolve(id)
        } else {
          reject(new Error('not found'))
        }
      }, 2000)
    
    })
}

  getRoles(user) {
    return new Promise((resolve, reject)=> {
      setTimeout(()=> {
        if (user=='cho') {
          resolve({name:'cho', role:'admin'})
        } else if(user=='kim') {
          resolve({name:'kim', role:'normal'})
        } else {
          reject(new Error('no access'))
        }
      }, 1000)
    })
  }
}

const userStorage = new UserStorage()
const id = prompt('아이디를 입력하세요!')
const password = prompt('비밀번호를 입력하세요')

userStorage.loginUser(id, password)
  .then(id => {
    console.log(`로그인에 성공했습니다.`)
    return userStorage.getRoles(id)
  })
  .then(userWithRoles=> {
    alert(`${userWithRoles.name}의 role은 ${userWithRoles.role}입니다.`)
  })
  .catch(console.log)
```

