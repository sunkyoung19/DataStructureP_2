# DataStructureP_2
<c++ 이용한 우선순위 큐 프로그래밍 방법>

1.노드 클래스 구현

class HeapNode
{
    int key;
 public:
    HeapNode(int k = 0): key(k){}
    void setKey(int k) {key = k;}
    int getKey(){return key;}
    void display() {cout << key;}
}


2.MaxHeap 클래스 구현

#include "HeapNode.h"
#define MAX_ELEMENT 200
 
class MaxHeap
{
  HeapNode node[MAX_ELEMENT];
  int size; 
public:
  MaxHeap( ) : size(0) { }
  bool isEmpty() { return size == 0; }
  bool isFull() { return size == MAX_ELEMENT-1; }
  
  HeapNode& getParent(int i){ return node[i/2]; } // 부모 노드 
  HeapNode& getLeft(int i) { return node[i*2]; } // 왼쪽 자식 노드 
  HeapNode& getRight(int i) { return node[i*2+1];} // 오른쪽 자식 노드
  
  void insert (int key){}// 삽입 함수
  HeapNode remove(){}// 삭제 함수
  HeapNode find() { return node[1]; }
}

3. 삽입함수 구현

void insert( int key )
{
  if( isFull() ) return;
  int i = ++size; // 증가된 힙 크기 위치에서 시작
  
// 트리를 거슬러 올라가면서 부모 노드와 비교하는 과정
  while( i!=1 && key>getParent(i).getKey()) {
    node[i] = getParent(i); // 부모 노드 끌어내림 (교환x)
    i/=2;
  }
  node[i].setKey( key );  // 최종위치에 데이터 복사
}

4. 삭제 함수

HeapNode remove() 
{
  if( isEmpty()) error();
  HeapNode item = node[1]; // 루트노드(꺼낼 요소)
  HeapNode last = node[size--]; // 힙의 마지막노드
  int parent = 1; // 마지막 노드 초기화
  int child = 2;  // 루트의 왼쪽 자식 위치 초기화
  while(child <= size){
    if (child <= size && getLeft(parent).getKey() < getRight(parent).getKey())
      child++
    if (last.getKey() >= node[child].getKey())
     
    node[parent] = node[child];
    parent = child;
    child *= 2;
  }
  node[parent] = last;
  return item;
  }
  
  STL 사용할 경우
 
 #include <queue>
 #include <functional>
 using namespace std;
  //내림차순
void heapSortDec( int a[], int n)
{
  priority_queue<int> maxHeap; 
  for(int i=0 ; i<n ; i++ )
        maxHeap.push(a[i]);
  for(int i=0 ; i<n ;i++ )
        a[i] = maxHeap.top();
        maxHeap.pop();
    }
}
  //오름차순
 void heapSortInc( int a[], int n)
{
  priority_queue<int, vector<int>, greater<int>> minHeap; 
  for(int i=0 ; i<n ; i++ )
        minHeap.push(a[i]);
  for(int i=0 ; i<n ;i++ )
        a[i] = minHeap.top();
        minHeap.pop();
    }
}
  
  
