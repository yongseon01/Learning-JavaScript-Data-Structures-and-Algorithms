
# Queue

## function
- enqueue(원소들): 큐의 뒤쪽에 원소들을 추가한다.
- dequeue(): 큐의 첫 번쨰 원소를 반환하고 큐에서 삭제한다.
- front(): 큐의 첫 번째 원소를 반환하되 큐 자체는 그대로 놔둔다.
- isEmpty(): 큐가 비어있으면 true를, 그렇지 않으면 false를 반환한다.
- size(): 큐의 원소의 개수를 반환한다. 배열의 length와 같다.

```javascript
function Queue(){
    var items = [];
    
    this.enqueue = function(element){
        items.push(element);
    };

    this.dequeue = function(){
        return items.shift();
    };

    this.front = function(){
        return items[0];
    };

    this.isEmpty = function(){
        return items.length === 0;
    };

    this.clear = function(){
        items = [];
    };

    this.size = function(){
        return items.length;
    };

    this.print = function(){
        console.log(items.toString());
    };
}
```

## 우선순위 큐
- 큐에 입력되는 원소에 우선순위를 부여해서 삭제(dequeue)) 순서를 결정
```javascript
function PriorityQueue(){
    var items = [];

    function QueueElement(element, priority){
        this.element = element;
        this.priority = priority;
    }

    this.enqueue = function(element, priority){
        var queueElement = new QueueElement(element, priority);

        if(this.isEmpty()){
            items.push(queueElement);
        }else{
            for(var i=0; i<items.length; i++){
                if(items[i].priority > queueElement.priority){
                    items.splice(i,0,queueElement);
                    break;
                }
                if(i === items.length-1){
                    items.push(queueElement);
                }
            }
        }
    };

    //아래부터는 일반 큐와 동일
    this.dequeue = function(){
        return items.shift();
    };

    this.front = function(){
        return items[0];
    };

    this.isEmpty = function(){
        return items.length === 0;
    };

    this.clear = function(){
        items = [];
    };

    this.size = function(){
        return items.length;
    };

    this.print = function(){
        for(var i=0;i<this.size();i++){
            console.log(items[i].element+'('+items[i].priority+')');
        }
    };
}

//test code
var priorityQueue = new PriorityQueue();
priorityQueue.enqueue("John",2);
priorityQueue.enqueue("Jack",1);
priorityQueue.enqueue("Camila",1);
priorityQueue.print();
```

## 환형 큐(뜨거운 감자 게임))
```javascript
function hotPotato(nameList, num){
    var queue = new Queue();

    for(i=0; i<nameList.length;i++){
        queue.enqueue(nameList[i]);
    }

    var eliminated = '';
    while(queue.size() > 1){
        for(var i=0;i<num;i++){
            queue.enqueue(queue.dequeue());
        }
        eliminated = queue.dequeue();
        console.log(eliminated + '를 뜨거운 감자 게임에서 퇴장 시킵니다.');
    }

    return queue.dequeue();
}

//test code
var names = ['John','Jack','Camila','Ingrid','Carl'];
var winner = hotPotato(names,7);
console.log('승자는 '+winner+' 입니다.');
```