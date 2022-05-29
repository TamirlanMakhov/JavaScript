# Выполненные задачи по JavaScript

1. Написать функцию, которая найдет и выведет в консоль юзеров, зарегистрированных 09.10.2021 и 10.10.2021). Массив в task1.txt 

Массив вида: 
```js
const users = [
  {
      firstName: 'John',
      lastName: 'Caper',
      phone: '7436676737634',
      registrationDate: '12.10.2021'
  }]
```

**Решение:**
```js
let NeededUsers = users.filter(i => i.registrationDate == "09.10.2021" || i.registrationDate === "10.10.2021");
console.log(NeededUsers);
```

2. Откройте в VSCode task2.json файл. Скопируйте из него JSONку, вставьте в свой код (присвоив в переменную).
Дан массив объектов. Каждый объект является идентификационной карточкой человека. Нам нужно хранить только уникальные значения в 
этом массиве. Реализуйте функцию, которая будет выполнять эту работу. 

Массив вида: 
```js
const idCards = [{
  "name": "Leanne Graham",
  "username": "Bret",
  "email": "Sincere@april.biz",
  "address": {
      "street": "Kulas Light",
      "suite": "Apt. 556",
      "city": "Gwenborough",
      "zipcode": "92998-3874",
      "geo": {
          "lat": "-37.3159",
          "lng": "81.1496"
      }
  },
  "phone": "1-770-736-8031 x56442",
  "website": "hildegard.org",
  "company": {
      "name": "Romaguera-Crona",
      "catchPhrase": "Multi-layered client-server neural-net",
      "bs": "harness real-time e-markets"
  }
}]
```

**Решение:**
```js
let tmpArray = [];

function itemCheck(item) {
    if (tmpArray.indexOf(item.name) === -1) {
        tmpArray.push(item.name);
        return true;
    }
    return false;
}


console.log(idCards.filter((item) => itemCheck(item))); 
```

3. Вывести все предприятия и их отделы. Рядом указать количество сотрудников. Для предприятия посчитать сумму всех сотрудников во всех отделах.

**Пример:**
Предприятие 1 (45 сотрудников)
- Отдел тестирования (10 сотрудников)
- Отдел маркетинга (20 сотрудников)
- Администрация (15 человек)
Предприятие 2 (75 сотрудников)
- Отдел разработки (50 сотрудников)
- Отдел маркетинга (20 сотрудников)
- Отдел охраны труда (5 сотрудников)
Предприятие 3 (нет сотрудников)
- Отдел аналитики (нет сотрудников)

Массив вида: 
```js
const enterprises = [{
    id: 1,
    name: "Предприятие 1",
    departments: [{
        id: 2,
        name: "Отдел тестирования",
        employees_count: 10,
      },
      {
        id: 3,
        name: "Отдел маркетинга",
        employees_count: 20,
      },
      {
        id: 4,
        name: "Администрация",
        employees_count: 15,
      },
    ]
  },
  {
    id: 5,
    name: "Предприятие 2",
    departments: [{
        id: 6,
        name: "Отдел разработки",
        employees_count: 50,
      },
      {
        id: 7,
        name: "Отдел маркетинга",
        employees_count: 20,
      },
      {
        id: 8,
        name: "Отдел охраны труда",
        employees_count: 5,
      },
    ]
  },
  {
    id: 9,
    name: "Предприятие 3",
    departments: [{
      id: 10,
      name: "Отдел аналитики",
      employees_count: 0,
    }, ]
  }
];
```

**Решение**:
```js
for (let i = 0; i < enterprises.length; i++) {
  let sums = 0;
  let sum = enterprises[i].departments.reduce(function (sums, currentValue) {
    return sums + currentValue.employees_count;
  }, sums);
  if (sum == 0) {
    sum = "нет";
  }
  console.log(`${enterprises[i].name}`, `(${sum} сотрудников)`);

  for (let j = 0; j < enterprises[i].departments.length; j++) { 
  console.log(`-${enterprises[i].departments[j].name}`, `${enterprises[i].departments[j].employees_count} сотрудников`);
  }
}
```


3. Написать функцию, которая будет добавлять отдел в предприятие. В качестве аргумента принимает id предприятия, в которое будет добавлен отдел и название отдела.

**Решение**:
```js
function addDepartment(myid, myname) {
  for (let i = 0; i < enterprises.length; i++) {
    for (let j = 0; j < enterprises[i].departments.length; j++) {
      if (enterprises[i].id == myid) {
        enterprises[i].departments[-1] = {};
        enterprises[i].departments[-1].id = 0;
        enterprises[i].departments[-1].name = myname;
      }
    }
  }
}
addDepartment(9, "Название нового отдела");
```


4.  Написать функцию для удаления отдела. В качестве аргумента принимает id отдела. Удалить отдел можно только, если в нем нет сотрудников.

**Решение**:
```js
function deleteDepartment(myid) {
  for (let i = 0; i < enterprises.length; i++) {
    for (let j = 0; j < enterprises[i].departments.length; j++) {
      if (enterprises[i].departments[j].id == myid && enterprises[i].departments[j].employees_count == 0) {
        delete enterprises[i].departments[j]; 
      }
    }
  }
}
deleteDepartment(10);
```

5.  Написать функцию для переноса сотрудников между отделами одного предприятия. В качестве аргумента принимает два значения: id отдела, из которого будут переноситься сотрудники и id отдела, в который будут переноситься сотрудники).

**Решение**: 
```js
function moveEmployees(from, to) {
  for (let i = 0; i < enterprises.length; i++) {
    for (let j = 0; j < enterprises[i].departments.length; j++) {
      if (enterprises[i].departments[j].id == from) {
        enterprises[i].departments[j].employees_count -= 1;
      } if (enterprises[i].departments[j].id == to) {
        enterprises[i].departments[j].employees_count += 1;
    }
  }
}}
moveEmployees(2, 3);
```

6. Дан массив объектов. Каждый объект является идентификационной карточкой человека. Нам нужно хранить только уникальные значения в этом массиве. Реализуйте функцию, которая будет выполнять эту работу.

Массив вида:
```js
const idCards = [{
	
	"name": "Leanne Graham",
	
	"username": "Bret",
	
	"email": "Sincere@april.biz",
	
	"address": {
	
		"street": "Kulas Light",
	
		"suite": "Apt. 556",
	
		"city": "Gwenborough",
	
		"zipcode": "92998-3874",
	
		"geo": {
	
			"lat": "-37.3159",
	
			"lng": "81.1496"

}

},

"phone": "1-770-736-8031 x56442",

"website": "hildegard.org",

"company": {

	"name": "Romaguera-Crona",
	
	"catchPhrase": "Multi-layered client-server neural-net",
	
	"bs": "harness real-time e-markets"

	}

}]
```

**Решение**:
```js
let tmpArray = [];

function itemCheck(item) {

	if (tmpArray.indexOf(item.name) === -1) {

		tmpArray.push(item.name);

		return true;
	}
	return false;
}

console.log(idCards.filter((item) => itemCheck(item)));
```
