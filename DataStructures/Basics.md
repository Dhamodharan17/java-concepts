**1.Volatile**
- indicates the content of the variable stored in main memory and every read done from main memory.
- indicated variable may be modified by different threads
- when declared volatile, java ensured to give latest write to any thread
  
**2. Transient**
- makes the variable exculde from serilization process for security, performance and compatibility.
- when serialized, transient variables will get default values of datatype.<br/>

**3. String Builder vs String vs StringBuffer**
- String - immutable,slow,string constant pool
- SBF - mutable, no thread safe, faster,heap
- SBD - mutable,threadsafe,slower then SBF
  
**4.String Pool**
-  string pool in Java is a special area in the Java heap memory that stores unique string literals.
  
  


   
