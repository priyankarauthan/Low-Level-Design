# Low-Level-Design

# LRU Cache
```
class LRUCache<K,V>
{
   private final int capacity;
   private final Map<K,Node<K,V>>cache;
   private final Node<K,V> head,tail;

   public static class Node<K,V>{
   K key;
   V value;
   Node<K,V> previous,next;
   
   Node(K key, V value){
     this.key = key;
     this.value = value;
     }
  } 
  public LRUCache(int initalCapacity)
  {
    this.initalCapacity = initalCapacity;
    this.cache = new HashMap<>(capacity);
    this.head = new Node<>(null,null);
    this.tail = new Node<>(null,null);
    head.next = tail;
    tail.previous = head;
  }

  public V get(K key)
  {
    if(!cache.containsKey(key))  return null;
    Node node = cache.get(key);
    removeFromNode(node);
    addToHead(node);
    return node.value;
  }

  public void put(K key,V value)
  {
    if(cache.containsKey(key)){
        Node node = cache.get(key);
        node.value = value;
        removeFromNode(node);
        addToHead(node);
      }
      else{
      Node newNode = new Node(key,value);
      cache.put(key,newNode);
      addToHead(newNode);
      if(cache.size()>capacity){
      removeFromNode(tail.previous);
      cache.remove(tail.previous.key);
        }
      }
  }

  public void addToHead(Node node){
    Node n1 = head.next;
    head.next = node;
    node.previous = head;
    node.next = n1;
    n1.revious = node;    
  }

  public void removeFromNode(Node node){
     node.previous.next = node.next;
     node.next.previous = node.previous;
     }
    
 ``` 


  

  
    
    
    
