# PDO-Wrapper-Class for PHP (MySQL/SQLlite)
A PDO Database Wrapper Class written in PHP providing CRUD methods and auto-schema mapping.

## Available Methods

### select($table, $where = "", $bind = "", $fields = "*", $entity_decode = true)

Example #1
    
    $results = $this->db->select("mytable");

Example #2

    $results = $this->db->select("mytable", "Gender = 'male'");
    
Example #3 with Prepared Statement
    
    $search = "John";
    $bind = array(
          ":search" => "%$search"
     );
    $results = $this->db->select("mytable", "FName LIKE :search", $bind);

### insert($table, $info)

If no SQL errors are produced, this method will return the number of rows affected by the INSERT statement.

Example #1:

    $insert = array(
          "FName" => "John",
          "LName" => "Doe",
          "Age" => 26,
          "Gender" => "male"
     );
     $this->db->insert("mytable", $insert);
     
### update($table, $info, $where, $bind = "")

 If no SQL errors are produced, this method will return the number of rows affected by the UPDATE statement.

 Example #1
 
     $update = array(
          "FName" => "Jane",
          "Gender" => "female"
     );
     $this->db->update("mytable", $update, "FName = 'John'");
    
Example #2 with Prepared Statement

     $update = array(
          "Age" => 24
     );
     $fname = "Jane";
     $lname = "Doe";
     $bind = array(
          ":fname" => $fname,
          ":lname" => $lname
     );
     $this->db->update("mytable", $update, "FName = :fname AND LName = :lname", $bind);

### delete($table, $where, $bind = "")

If no SQL errors are produced, this method will return the number of rows affected by the DELETE statement.
     
Example #1

     $this->db->delete("mytable", "Age < 30");
    
Example #2 with Prepared Statement

     $lname = "Doe";
     $bind = array(
          ":lname" => $lname
     )
     $this->db->delete("mytable", "LName = :lname", $bind);
     
### Misc Functions

#### filter($table, $info)
Automated table binding for MySql or SQLite.

#### setErrorCallbackFunction($errorCallbackFunction, $errorMsgFormat = "html")

The error message can be displayed, emailed, etc within the callback function.
     
Basic Example:
     
      function myErrorHandler($error) {
      }
      
      $db = new db("mysql:host=127.0.0.1;port=0000;dbname=mydb", "dbuser", "dbpasswd");
      $this->db->setErrorCallbackFunction("myErrorHandler");
     
Text Version

      $this->db->setErrorCallbackFunction("myErrorHandler", "text");
      
      // Use Built-In PHP Function
      $this->db->setErrorCallbackFunction("echo");

#### debug()
A better PDO debugger, just because. Nicely styled CSS Error output.

     // If no other error handler is defined, then use this.
     if (!empty($this->errorCallbackFunction)) {
     ...
     }