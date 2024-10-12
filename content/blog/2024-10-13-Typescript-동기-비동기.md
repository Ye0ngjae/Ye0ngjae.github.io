---
title: "[Typescript] 동기 비동기"
dateString: October 2024
draft: false
tags:
  [
    "Typescript",
    "Javascript",
    "동기",
    "비동기",
    "Callback",
    "Promise",
    "Async/Await"
  ]
weight: 10
date: 2024-10-13
categories: ["Typescript", "Javascript"]
# cover:
    # image: ""
---
# 동기와 비동기
---
동기가 작업의 처리가 완료되었는지 여부를 확인하고 다음 작업을 수행한다면, 비동기는 작업의 완료 여부와 상관없이 바로 다음 작업을 수행하는 것을 말한다.

Javascript는 **단일 스레드 언어**이다. 이는 Javascript가 작업을 수행할 때 CPU가 프로그램을 동작시키는 최소 단위인 스레드를 하나밖에 사용하지 않는다는 뜻이다. 만일 웹 서버에서 동기 API를 사용할 경우 웹 서버는 해당 동기 API의 작업 수행을 완료하여 결괏값을 반환하기 전까지 일시적으로 멈추기 때문에 웹 서버의 반응성을 떨어뜨릴 수 있다.

따라서 웹 서버를 개발하면서 일정 시간 이상이 소요되는 작업을 수행할 때, 동기 API의 사용을 최대한 지양해야 하며, 비동기 API를 사용하여 이러한 문제점을 해결하는 편이 좋다.

하지만 비동기로만 코드를 작성할 경우 다른 문제가 발생할 수 있다.

```js
function getDB() {
    let data;
    // 데이터베이스에서 값을 가져오는 3초 걸린다고 가정 (비동기 처리)
    setTimeout(() => {
        data = 100;
    }, 3000);

    return data;
}

function main() {
    let value = getDB();
    value *= 2;
    console.log('value의 값 : ', value);
}
main(); // 메인 스레드 실행

// 실행 결과
// value의 값 : NaN
```

위 코드의 실행 결과를 보면, 원래 3초 뒤에 100이라는 값이 반환되고 * 2 연산이 진행되어 200이 출력되어야 했지만,  getDB 함수가 실행되고 setTimeout이라는 비동기 함수가 실행되었음에도 value의 값에는 NaN가 들어가 있다.

이는 비동기 함수를 실행했을 때, 결과가 들어오지 않더라도 바로 다음 코드를 실행해 버리기 때문에 발생하는 문제이다. 하지만 꼭 비동기로 작업의 순서를 맞추며 작업을 수행해야 하는 경우 callback 함수, Promise, Async/Await 등의 방법을 고려해 볼 수 있다.

## Typescript와 Javascript

Typescript는 실행될 때 NodeJS나 브라우저는 Javascript만 읽어드릴 수 있기 때문에 Javascript로 Transpile하는 과정이 필요하다. Typescript 파일을 실행하게 되면 Typescript 파일은 tsconfig를 통해서 Javascript로 Transpile되어 동작한다.

# Callback

앞서 말한 비동기 처리에서의 작업 순서 문제를 해결하기 위해 처음 나온 것이 바로 Callback 함수이다. Callback 함수는 함수의 매개변수에 함수 자체를 넘겨, 함수 내에서 매개변수인 함수를 실행하는 기법이다.

```js
function getDB(callback) {
    // 데이터베이스로부터 3초 후에 데이터 값을 받아온 후, 콜백 함수 호출
    setTimeout(() => {
        const value = 100;
        callback(value);
    }, 3000);
}

function main() {
    // 호출할 작업에 콜백 함수를 넘긴다
    getDB(function(value) {
        let data = value * 2;
        console.log('data의 값 : ', data);
    });
}
main();

// 실행 결과
// value : 200
```

위 코드는 callback 함수 내에서 data 변수의 값을 받아 출력하므로, 비동기 작업이 완료된 후에 data의 값을 출력하게 된다. callback 함수는 비동기 함수에서 작업 결과를 전달받아 처리하는데 사용되어 작업 순서를 맞출 수 있게 된다.

하지만 다수의 비동기 작업이 필요할 때 callback 함수를 사용할 경우 callback 함수 안에 callback 함수 안에 callback 함수 안에 callback 함수가 들어가며, 코드의 모양이 > 가 되어가는 광경을 목격할 수 있다. 이는 코드를 읽기 어렵게 만들며, callback지옥에 빠질 수 있게 한다.

# Promise

callback 함수는 정식적으로 비동기를 순차적으로 이용할 수 있게끔 제공하는 기능이 아니라 일종의 편법이다. Promise는 비동기 작업의 순차적 처리를 위해 만들어진 객체이며, 비동기 작업의 성공 또는 실패와 그 결괏값을 나타내는 객체이다. `.then()`과 `.catch()` 를 이용하여 비동기 작업 이후 진행될 다른 작업의 처리를 진행한다.

```js
function getDB() {
  return new Promise((resolve) => {
    setTimeout(() => {
      const value = 100;
      resolve(value);
    }, 3000);
  });
}

function main() {
  getDB()
    .then((value) => {
      let data = value * 2;
      console.log('data의 값 : ', data);
    })
    .catch((error) => {
      console.error(error);
    });
}

main();
```

하지만. then()을 이용하여 순차 처리를 진행하기 때문에 callback 지옥과 같이 promise 또한 promise 지옥에 빠질 수 있다.

# Async / Await

async와 await은 이러한 문제를 해결하기 위하여 추가되었으며, promise를 기반으로  동기 프로그램을 작성하듯이 간편하게 프로그래밍이 가능하다. 또한, 항상 Promise의 형태로 값을 반환하기 때문에 일반 함수처럼 사용할 수 있지만 Promise 객체로도 사용할 수 있다.

```js
function getDB() {
    return new Promise((resolve, reject) => {
        // 데이터베이스에서 값을 가져오는 3초 걸린다고 가정 (비동기 처리)
        setTimeout(() => {
            const value = 100;
            resolve(value); // Promise 객체 반환
        }, 3000);
    });
}

async function main() {
    let data = await getDB(); // await 키워드로 Promise가 완료될 때까지 기다린다
    data *= 2;
    console.log('data의 값 : ', data);
}
main(); // 메인 스레드 실행
```

## 참고

- [https://inpa.tistory.com/entry/🌐-js-async#비동기의_병렬_처리_원리](https://inpa.tistory.com/entry/%F0%9F%8C%90-js-async#%EB%B9%84%EB%8F%99%EA%B8%B0%EC%9D%98_%EB%B3%91%EB%A0%AC_%EC%B2%98%EB%A6%AC_%EC%9B%90%EB%A6%AC)
- [https://velog.io/@ko1586/Callback함수란-뭔데](https://velog.io/@ko1586/Callback%ED%95%A8%EC%88%98%EB%9E%80-%EB%AD%94%EB%8D%B0)
- [https://velog.io/@skulter/TypeScript-7.-Promise와-asyncawait-구문](https://velog.io/@skulter/TypeScript-7.-Promise%EC%99%80-asyncawait-%EA%B5%AC%EB%AC%B8)