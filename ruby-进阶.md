#ruby进阶的学习(高级)
##number and text
###number

```
	a.Fixnumber
		foo = 23
		foo.class #=>Fixnum
	b.Bignumber
		foo = 1_000_000_000_000_00
	 	foo.class #=>Bignum	
	c.even	
		foo = 2
		foo.even? #=>true
		foo = 3
		foo.odd? #=>true
	d.to_s
		foo = 123
		foo.to_s #=>"123"
	e.round 
		foo = "2.34545454"
		foo.round(2) #=> 2.34
```
##ruby naming
###varible,symbol,method:snake_case
- **constant:CONST_FOO**

- **class name: CamelCase**

- **filename:file_name.rb**

###method usege
```
a.%q
	%q('abc'afaafdf'') #=>"'abc'afaafdf''"
b.%Q
	%Q('abc'afaafdf'') #=>"\"abc'afaafdf'\""
c.reverse
	a = "abc"
	a.reverse #=> "cba"
d.<<-TEXT;TEXT
	<<-TEXT
	abc
	abc
	abc
	TEXT
						#=>"abc\nabc\nabc"
e.include
	"hellow".include?("e") #=>true
f.index
	"hellow".index('l')    #=>2
g.sub and gsub
 	"hellow".sub('l','')  #=>"helow"
	"hellow".gsub('l','') #=>"heow"
```
##class usege

```
class Point  #CamelCase --contant
	attr_accessor :x  #getter and setter
	attr_accessor :y	 #getter
	def initialize(x = 0, y = 0)
		#@x instance variable
		#@@x class variable
		#$x global variable
		#x	lcoal variable
 		@x,@y = x,y 
	end
	
	def first_quadrant?
		 x > 0 && y > 0
	end
	
	def +(p2)
		Point.new(x + p2.x, y + p2.y )
	end
end
p1 = Point.new(x = 2, y = 3)
p2 = Point.new(x = 3, y = 2)
p1 + p2  #=><Point:0x007ff9aa878790 @x=6, @y=8>

```
##Symbol and Array
##symbol
```

```
##Array

```
define method
	a.a = []
	b.a = Array.new
	c.a = Array.new(3) #=>[nil, nil, nil]
	d.a = Array.new(3,0) #=>[0, 0, 0]
	e.a = Array.new(3){"abc"} #=>["abc","abc","abc"]
	f.a = %w(foo bar dog cat) #=>["foo", "bar", "dog", "cat"]
Array use
	a = Array.new(3,"abc")   #=>["abc", "abc", "abc"]
	a[0]       #=> "abc"
	a[0][0] = "b"   #=>"b"
	a  #=> ["bbc", "bbc", "bbc"]
	解决方法:
	a = Array.new(3){"abc"}
	a[0].object_id #=>70355142461380
	a[1].object_id #=>70355142461360
	a[0][0]= "b"
	a #=>["bbc", "abc", "abc"]	
	method use
	a = ["abc","bcd","cde","def"]
	a[0]     #=>"abc"
	a[2..3]  #=>["cde", "def"]
	a.fetch(0)  	#=>"abc"
	a.fetch(5)	#=>error
	a.fetch(5,"cba") #=>"cba"
	a.include("abc")?  #=>true
	a.empty? #=>flase
	a.push("efg") #=>=> ["abc", "bcd", "cde", "def", "efg"]
	a.delete_at(0)   #=>["bcd", "cde", "def", "efg"]
	a.delete("efg")  #=>["bcd", "cde", "def"]
	a[10]   #=>["bcd", "cde", "def", nil, nil, nil, nil, nil, nil, nil, "aaa"]
	a.uniq!  ＃＝>["bcd", "cde", "def", nil, "aaa"]
	a.shuffle #=>["aaa", nil, "def", "bcd", "cde"]
	
	a =[[1,2,3,4],[3,4]]
	a.flatten #=>[1, 2, 3, 4, 3, 4]
	a = [1,2,3,4,5]
	a.each {|a| p a}   #=>1 2 3 4 5
	a.reverse_each{|a| p a} #=>5 4 3 2 1
	
	a = [-4,1,-2,3-,5]
	a.sort!     ＃＝>[-4, -3, -2, 1, 5]
	a.select{|e| e>1}  #=>[5]
	a<<"nil"
	a   #=>[-4,1,-2,3-,5,nil]
	a.compact!        #=>[-4, 1, -2, -3, 5]
	a.any?{|e| e>5}   #=>false
	a.any?{|e| e<5}   #=>true
```
##Hash,Set

###Hash

```
define method
	symbol write
 		a = {key: value}   		#=> {:key=>"value"}
 		a = {:a => "value"} 	#=>{:a=>"abc"}
		a = {}					  	#=>{}
		a = Hash.new
		a = Hash.new(3)			#=>a[anynumber]=3(init value)		
		a = Hash.new([])			#=>	{}
		a[:a] << 1
		a[:a]                	#=>[1]
		a[:b]						#=>[1]
		解决方法:
		a = Hash.new {|h,k| h[k] = []} 	#=>{}
		a[:a]<<1
		a[:a] = [1]
		a[:b] = []    
	String write
		a = {"bac" => "cba"} 	#=>{"bac"=>"cba"}
method use
	a = {a: 1, b:2}
	a[:c] = 3
	a       				#=>{:a=>1, :b=>2, :c=>3}
	a.delete(a)  			#=>{:b=>2, :c=>3}
	a.assoc(:b)  			#=>[:b, 2]
	a.empty?				#=>false
	a.has_value?(2) 		#=>true
	a.has_key?(:b)    	#=>true
	a.values   			#=>[2, 3]
	a.keys					#=>[:b, :c]
	a.to_a					#=> [[:b, 2], [:c, 3]]
	
	merge
		h1 = {a: 1}
		h2 = {b: 2,c: 3}
		h = h1.merge(h2)    #=>{:a=>1, :b=>2, :c=>3}
	each
		h.each {key,value p[key.value]}  	#=>[:a, 1]
												   [:b, 2]
												   [:c, 3]
		h.each_value{|v| p v}				#=>1
												   2
												   3
		h.each_key{|k| p k}					#=>:a
												   :b
												   :c
		h.select{|key| key==:a}				#=>{:a=>1}

```	
###set

```
define set
	first: require "set"    	#=>true
	set.new[1,2]
	s = _							#=><Set: {1, 2}>
	a.add("foo") 					#=> #<Set: {1, 2, "foo"}>
	h = Set.new [2,3,4,"foo"] 		#=> #<Set: {2, 3, 4, "foo"}>
	s & h                        	#=>#<Set: {2, 3,"foo"}>
	s | h							#=>#<Set: {1, 2, 3, 4, "foo"}>
	s <= h							#=>flase
	h <= s							#=>false
	a = Set.new [2,3]
	b = Set.new [2,3,5] 
	a <= b   						#true
``` 

###Range
	
```
	..
		r = 1..2
		r.include?(2)   #＝>true
	...
		r = 1..2
		r.include?(2)   #=>flase
		a = [1,3,5,6,7]
		a[1..2]      		#=>[3,5]
```
	
- **Homework**

	
	`如何解决Hash中的String和sysble作为key的互换问题`
	
##Ruby methods
###ruby iterator and block
```
	[1,2,3].each do |elem|
		puts elem
	end
```

- **block best practice** `multi-line use do...end,one-line use{...},{...}has high prioity than do...end`

	```
	arr.each do |elem|     scope :foo, lambda{ |elem|									foo(elem)	
		foo(elem)					bar(elem)
		bar(elem)					baz(elem)
		baz(elem)				}
	end
	
	arr.each{|elem| puts elem}
	```

###Proc class include `proc and lambda object` 

- **proc**

	```
		arr  = %w(a b c)     			#=> ["a", "b", "c"]
		arr.map(&:capitalize) 			#=> ["A", "B", "C"]
		arr.map{|x| x.capitalize}		#=> ["A", "B", "C"]
		
		proc = Proc.new{|x| x * 2}
		proc.call(2)		        #=>4
		proc.class               #=>Proc
	```
- **lambda**
	
	```
	lambda = lambda{|x| x*2}
	lambda.call(2)          #=>4
	lambda.class            #=>Proc
	```
- **Differences between proc and lambda**
####Differences 1:parameters
	```
	p = Proc.new{|x,y|p x,y}		#=><Proc:0x007f9302294b58@(irb)
	p.call(1)    						#=> [1, nil]
	p.call(1,2)						#=> [1, 2]
	p.call(1,2,3)						#=> [1, 2]
	
	
	p = lambda{|x,y|p x,y}			#=><Proc:0x007f930226f5b0@(irb):88 (lambda)>
	p.call(1)							#=>error
	p.call(1,2)						#=> [1, 2]
	p.call(1,2,3)						#=>error
	```
 `Summary: proc behaves more like a block, lambda behaves more like a method`
 
 ####Differences 2:flow control
 
 ```
	p = Proc.new{ |x| return if x>0}   	#more like a block
	p.call(1)                           #=>error
		
	l = lambda{ |x| return ""if x>0}        #<Proc:0x007f93021ee9b0@(irb):98 (lambda)>	
	l.call(1)									#=> ""
 ```	

##Class and Method
```
class Point               #CamelCase --contant

end
p = Point.new
p.methods(false)                 # =>[]
Point.ancestors                  # =>[Point, Object, Kernel, BasicObject]


class Point    #CamelCase --constant
	attr_accessor :x  #getter and setter
	attr_reader :y    #getter
	
	@@origin = 0    ＃封装性
	ORIGIN = 0		＃Ponit::raORIGIN
	def initialize(x=0,y=0)
		#@instant variable
		#@@ class variable
		#$x global variable
		#x local variable
		@x,@y = x,y
	end

	def first_quadrant?
		#self.x > 0 && self.y > 0
		x>0 && y > 0 
	end

	def +(p2)
		Ponit.new(x+p2.x,y+p2.y)
	end
	
	＃class method 
	def self.second_quadrant(x,y)?
		x < 0 && y > 0 
	end
	#class methods
	
	class << self
		def foo
		
		end
		
		def bar
		
		end
		
		def wat
		
		end
	end
end
Point.second_quadrant(x,y)?
Point.foo
Point.bar 
Point.wat
```
##private and protected differences

**differences table**

|            	|  visibility	| inheritance| call on obj|
| :--------: 	| :--------:	| :----: 	|:----------:|
| public  	| in/out of the cllass|  yes |     yes    |
| private    	|   within 	|  yes 	|       yes  |
| protected  	|   within 	| yes  	|No(implicitly call)|

**For example**

```
class Point
	attr_accessor :x
	attr_accessor :y
	def initialize(x=0,y=0)
		@x,@y = x,y
	end

	def first_quarant?
		 x > 0 && y>0 
	end

	private :first_quarant?

	def second_quadrant?
		x > 0 && y>0
	end
	protected :second_quadrant?

	def bar
		first_quarant?
		second_quadrant?
	end

	def wat
		self.second_quadrant?
	end

	def wut
		self.first_quarant?    #＝>oMethodError: private method `first_quarant?' called for #<Point:0x007fea011d2278 @x=0, @y=0>
	end
end

```
**Inheritance**

```
class Point3D < Point
	def initizlize(x=0,y=0,z=0)
		supper(x,y)        #supper(x,y,z)
		@z = z
	end
end

p = Point3D.new
p.is_a?Point      	#=>true
p.is_a?Point3D		#=>true	
p.instance_of? Point          	#=>false
p.instance_of? Point3D				#=>true
Point3D.superclass					#=>Point
Point3D.ancestors              	#[Point3D,Point, Object, Kernel, BasicObject]
```
**For example**

```
class BankAccount
	attr_render :balance
	@@exchange_rate = 6.2
	def initialzie(amount = 0)
		@balance = amount
	end
	#class method
	class << self
		def usd_to_rmb(amount)
			(amount * @@exchange_rate).round(2)
		end
		
		def rmb_to_usd(amount)
			(amount / @@exchange_rate).round(2)
		end
	end
	
	def deposite(amount)
		@balance += amount
	end
	
	def	withdrow(amount)
		@balance -= amount
		raise "Overdraw Alert" if @balance < 0
	end
end
```

##Module

```
module Helper
	#获取两点之间的距离
	def self.distance(obj1,obj2)
		Math.sqrt((obj1.x - obj2.x) ** 2 +(obj1.y - obj2.y) **2 )
	end

	def shift_right(x,y,z=0)
		puts x+3,y,z
	end
end
```
###Mixin Ruby Moudle
	
**include:mixin module instance methods as class'instance methods**
**extend:mixin module instance methods as class'class methods**

##singleton method and methods's find

- **singlton method defined on object(supper class of singleton class)**
- **instance method defined in class**
- **instance method defined in moudle (reverse order in which they were include)**
- **instance method define in ancestors**
- **method_missing defined in Kernel module**

subclass of --->instance of --->include ---> moudlue(oder by Desc) --->class

**For example**

file1:`helper.rb`

```
module C
	def foo
		puts 'foo in C'
	end
end

module D
	def foo
		puts 'foo in D'
	end
end
#### class ###
class A
	def foo
		puts 'foo in A'
	end
end

class B < A
	include C
	include D
	def foo
		puts 'foo in B'
	end
end
```
file2:`method_singleton.rb`

```
a = A.new
b = B.new

def b.foo
	puts "singleton foo"
end
a.foo
b.foo
```






 　






 