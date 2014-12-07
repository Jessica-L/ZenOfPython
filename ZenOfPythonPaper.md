#The Zen of Python and Its Application  
###Readability Promotes Reusable Code  

  
CSCI 3155 Principles of Programming Languages  
  
Jessica Lynch  
Noah Dillon   
Max Harris  

Python is highly readable due to its complete set of Style guidelines and Pythonic idioms relayed in detail in the  
Process Python Enhancement Proposal (PEP) #8, "Style Guide for Python Code" created by GvR, Warsaw and Coghlan in  
2001.  On August 19, 2004, "The Zen of Python" by Pythoneer Tim Peters was approved as Informational PEP 20. While  
PEP 8 is all about the rules for structuring your code, PEP 20 conveys the inspiration behind how you write your  
Python code. You can access The Zen of Python by visiting https://www.python.org/dev/peps/pep-0020 or via the Python  
terminal or command prompt by typing >>import this and pressing Enter.  The below list of Python Zen points will  
print to the screen unnumbered.  
  
	1. Beautiful is better than ugly.  
	2. Explicit is better than implicit.  
	3. Simple is better than complex.  
	4. Complex is better than complicated.  
	5. Flat is better than nested.  
	6. Sparse is better than dense.  
	7. Readability counts.  
	8. Special cases aren't special enough to break the rules.  
	9. Although practicality beats purity.  
	10. Errors should never pass silently.  
	11. Unless explicitly silenced.  
	12. In the face of ambiguity, refuse the temptation to guess.  
	13. There should be one-- and preferably only one --obvious way to do it.  
	14. Although that way may not be obvious at first unless you're Dutch.  
	15. Now is better than never.  
	16. Although never is often better than *right* now.  
	17. If the implementation is hard to explain, it's a bad idea.  
	18. If the implementation is easy to explain, it may be a good idea.  
	19. Namespaces are one honking great idea -- let's do more of those!  
  
Python according to its creator Guido van Rossum provides a higher level of readability aimed at the creation of  
reusable code.  Guido writes in his original Python Style Guide essay, "... code can hardly be considered reusable if  
it's not readable."  In industry, reusable code is coveted to help achieve time and memory efficiency.  Why reinvent  
code that has already been written?  This is not a hypothetical question.  Here are the main reasons programmers opt  
to write their own version of pre-existing code:  

	(1) The code (despite doing its job) is badly written -- sloppy, too implicit, etc... or simply put, a hack job!  
	(2) The code is hard to understand (perhaps, just too complex and/or missing comments) even though it is doing its job.  
	(3) The programmer is in too big of a hurry and can code up quickly what s/he needs.  
  
Let's focus on statements (1) and (2) because they often bring about statement (3).  Statements (1) and (2) in the  
case of Python are the result of one or more violations of the Python style guidelines (PEP 8) which are summarized  
in the Zen of Python (PEP 20).  
  
The first seven Zen points of PEP 20 address the beautiful nature of Python code if written well, that is according  
to the Zen of Python. To illustrate, we will analyze the below code examples based on the task of walking a directory  
tree containing multiple directories to generate a list of all filepaths of files contained within.  Our first example  
violates several of the Zen points 1 - 7 and we progressively improve upon this example with our second (better) and  
third (best) examples.  

Example 1:  
  
````python  
import os.path as op

def generate_file_list( filepath ):
   pathList = []
   path0    = filepath
   dirList0 = os.listdir( path0 )

   for p0 in dirList0:
      path1 = op.join( path0, p0 )
      if op.isdir( path1 ):
         dirList1 = os.listdir( path1 )

         for p1 in dirList1:
            path2 = op.join( path1, p1 )
            if op.isdir( path2 )
               dirList2 = os.listdir( path2 )

               for p2 in dirList2:
                  path3 = op.join( path2, p2 )
                  if op.isdir( path3 ):
                     dirList3 = os.listdir( path3 )

                     for p3 in dirList3:
                        path4 = op.join( path3, p3 )
                        if op.isdir( path4 ):
                           dirList4 = os.listdir( path4 )

			   for p4 in dirList4:
                              pathList.append( op.join( path4, p4 ) )

                        else: 
                          pathList.append( op.join( path3, p3 ) )

                  else:
                     pathList.append( op.join( path2, p2 ) )

             else:
                pathList.append( op.join( path1, p1 ) )

      else:
         pathList.append( op.join( path0, p0 ) )

   return pathList                 
````
  
Example 1, although it may save memory by avoiding recursion, fails to adhere to Zen points 1, 3, 5 and 6, which  
furthermore, hinders readability and fails to adhere to Zen point 7.  
  
  
Example 2:  
````python 
import os.path as op

def generate_file_list( filepath ): 
   pathList = []
   for root, dirs, files in os.walk( filepath ):
      for filename in files:
         pathList.append( op.join(root, filename) )
      for dir in dirs:
         generate_file_list( dir )
   return pathList
````  
  
  
Example 2 is a lot more readable due to its simplicity achieved through less lines of code.  However, it does a lot  
of unnecessary work behind the scenes.  Python's os.walk module is useful to lessen lines of code, but when dealing  
with big data i.e. millions of lines of code to traverse and analyze, the implementation of this module which uses  
recursion can be expensive.  
  
  
Example 3:  
````python  
import os.path as op

def generate_file_list( filepath ):
   pathList = []
   if op.isdir( filepath ):
      for p0 in os.listdir( filepath ):
         path1 = op.join( filepath, p0 )
         if op.isdir( path1 ):
            pathList += generate_file_list( path1 )
         else:
            pathList.append( path1 )
   return pathList
````  
  
Example 3 is in one way or another beautiful, explicit, simple, flat and sparse, and is therefore readable making it  
reusable code which adheres to the Zen of Python points 1 through 7.  
  
  
Now, we will move on to briefly explain the remaining Zen of Python points.  
  
   
  
Resources:
http://docs.python-guide.org/en/latest/writing/style/  
http://ruben.verborgh.org/blog/2013/02/21/programming-is-an-art/  
https://www.python.org/doc/essays/foreword/ (Guido van Rossum's original Python Style Guide essay)  
http://neopythonic.blogspot.com/ (Guido's blog)  
http://www.stat.washington.edu/~hoytak/blog/whypython.html  