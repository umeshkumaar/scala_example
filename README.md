# scala_example
create_binary_tree_using_scala

//code
package umesh_mittal

object binary_tree {
val t1=new nonEmpty(3,new Empty,new Empty)        //> t1  : week3.nonEmpty = {.3.}
val t2= t1 incl 4                                 //> t2  : week3.IntSet = {.3{.4.}}
val t3= t2 incl 1                                 //> t3  : week3.IntSet = {{.1.}3{.4.}}
val t4= t3 incl 10                                //> t4  : week3.IntSet = {{.1.}3{.4{.10.}}}
val t5= t4 incl 7                                 //> t5  : week3.IntSet = {{.1.}3{.4{{.7.}10.}}}

}

abstract class IntSet {

  def incl(x: Int): IntSet
  def contains(x: Int): Boolean
}

class Empty extends IntSet {

  def contains(x: Int): Boolean = false
  def incl(x: Int): IntSet = new nonEmpty(x, new Empty, new Empty)
	override def toString="."
}

class nonEmpty(elem: Int, left: IntSet, right: IntSet) extends IntSet {

  def contains(x: Int): Boolean =
    if (x < elem) left contains x
    else if (x > elem) right contains x
    else true

  def incl(x: Int): IntSet = {
    if (x > elem) new nonEmpty(elem, left, right incl x)
    else if (x < elem) new nonEmpty(elem, left incl x, right)
    else this
  }
   override  def toString= "{" + left + elem + right +"}"
  
}
