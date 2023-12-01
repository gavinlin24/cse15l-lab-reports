# Lab Report 5

## Student Question
I am having trouble compiling TestListExamples. The error message in the terminal says the junit package doesn't exist, so I think there is something wrong when I tried to copy the lib folder into the student-submissions directory.


## TA Response
What options can be used with the cp command to copy a directory and its contents? 

## Information Received

## Setup Information Needed
file and directory structure:

**grade.sh**
```
CPATH='.;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo "finished cloning"

path=`find student-submission -name ListExamples.java`

if [[ -e $path ]]
then
    echo "ListExamples.java found"
else
    echo "ListExamples.java not found"
    exit
fi

# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests

cp student-submission/ListExamples.java grading-area
cp TestListExamples.java grading-area
cp lib grading-area

cd grading-area
javac -cp $CPATH *.java

if [[ $? -ne 0 ]]
then
    echo "ListExamples.java could not compile"
    exit
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples
```

**TestListExamples.java**
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;
import java.util.ArrayList;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {
  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }

  @Test
  public void testMerge(){
    ArrayList<String> input1 = new ArrayList<String>();
    ArrayList<String> input2 = new ArrayList<String>();
    input1.add("a");
    input1.add("d");
    input2.add("b");
    input2.add("c");

    ArrayList<String> output = new ArrayList<String>();
    output.add("a");
    output.add("b");
    output.add("c");
    output.add("d");

    assertEquals(output, ListExamples.merge(input1, input2));
  }

  @Test
  public void testFilter(){
        ArrayList<String> input1 = new ArrayList<String>();
        input1.add("MOON");
        input1.add("sun");
       
        ListExamples.filter(input1, new IsMoon());

        ArrayList<String> output = new ArrayList<String>();
        output.add("MOON");

        assertEquals(output, input1);


  }
}
```
commands to trigger bug:
fixing the bug:
