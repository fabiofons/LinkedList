# Linkedlist 
```javascript
function NodeList(val, ref) {
    this.val = val;
    this.ref = ref
}

// Constructor function Linkedlist 
function LinkedList() {
  this._head = null;
  this._tail = null
  this._length = 0;
  this._valArr = [];
}
  
//Add a element to the LinkedList
LinkedList.prototype.add = function(val) {
  let node = new NodeList(val);
  if(!this._head) {
      this._head = node;
      this._tail = node;
      this._valArr.push(node.val);
  } else {
      this._tail.ref = node;
      this._tail = node;
      this._valArr.push(node.val);
    }
  this._length++;
}

// For get the length of the list.
LinkedList.prototype.length = function () {
  return this._length;
}
  
//Add a value in a specific position.
LinkedList.prototype.addAt = function(pos, val) {
  if(pos > this._length){
    return 'The position that you insert is not valid';
  
  } else if(pos === 0) {
    let node = new NodeList(val);
    node.ref = this._head.ref;
    this.head = node;
    this._valArr.splice(pos,0,val)

  } else {
    let reference = this._head;

    for(let i = 1; i < pos; i++){
      reference = reference.ref;
    }

    let node = new NodeList(val, reference.ref);
    reference.ref = node;
    this._valArr.splice(pos,0,val);
  }
  this._length++
}
  
//valueAt Get the value from the Linkedlist
LinkedList.prototype.valueAt = function(pos) {
  let reference = this._head
  if(pos >= this._length){
    return 'The position that you insert is not valid';  
  }
  if(pos === 0) {
    return reference.val;
  
  } else {
    for(let i = 0; i < pos; i++) {
      reference = reference.ref;
    }
    return reference.val;
  }
}
  
//Remove a node from the Linkedlist
LinkedList.prototype.remove = function(pos) {
  let reference = this._head;
  let refPrevtoDel = null
  if(pos >= this._length){
    return 'The position that you insert is not valid';

  } else if(pos === 0) {
    reference = reference.ref;
    this._head = reference;
    

  } else {
    for(let i = 1; i < pos; i++){
      reference = reference.ref;
    }

    refPrevtoDel = reference;

    if(pos === this._length - 1){
      this._tail = refPrevtoDel;
      refPrevtoDel.ref = undefined;              
    } else {        
      reference = reference.ref;
      refPrevtoDel.ref = reference.ref;
    }
  } 
  this._length--;
  this._valArr.splice(pos, 1)
}
  
//Reverse.. change the order of nodes
LinkedList.prototype.reverse = function() {
  let reference = this._head;
  let refNodes = {};
  const length = this._length;
  this._valArr.splice(0, length - 1);

  for (let i = 0; i < this._length; i++){
    refNodes[i] = reference.val;
    reference = reference.ref;      
  }

  this._head = this._tail;   
  for (let i = this._length - 2; i >= 0; i--){
    this.add(refNodes[i]);
  }
  this._length = length;
}

// Method Middle for get a value in the middle of the list
LinkedList.prototype.middle = function() {
  const reference = this._valArr.length;
  const half = Math.floor(reference / 2);
  if(reference % 2 === 0) {
    return this._valArr[half - 1];
  } else {
    return this._valArr[half];
  }  
}
```
