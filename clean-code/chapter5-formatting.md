# Formatting
You should take care that your code is nicely formatted. You should choose a set of simple rules that govern the format
 of your code, and then you should consistently apply those rules. If you are working on a team, then the team should 
 agree to a single set of formatting rules and all members should comply. It helps to have an automated tool that can 
 apply those formatting rules for you.


## 1. The Purpose of Formatting
First of all, let’s be clear. Code formatting is important. It is too important to ignore and it is too important to 
treat religiously. Code formatting is about communication, and communication is the professional developer’s first 
order of business.

### Vertical Openness Between Concepts
Nearly all code is read left to right and top to bottom. Each line represents an expression or a clause, and each 
group of lines represents a complete thought. Those thoughts should be separated from each other with blank lines.

There are blank lines that separate the package declaration, the import(s), and each of the functions. This extremely
 simple rule has a profound effect on the visual layout of the code. Each blank line is a visual cue that identifies a
  new and separate concept. As you scan down the listing, your eye is drawn to the first line that follows a blank line.

### Vertical Density
If openness separates concepts, then vertical density implies close association. So lines of code that are tightly 
related should appear vertically dense.

Concepts that are closely related should be kept vertically close to each other. Clearly this rule doesn’t work for
 concepts that belong in separate files. But then closely related concepts should not be separated into different 
 files unless you have a very good reason. Indeed, this is one of the reasons that protected variables should be 
 avoided.

### Vertical Ordering
In general we want function call dependencies to point in the downward direction. That is, a function that is called 
should be below a function that does the calling.2 This creates a nice flow down the source code module from high level 
to low level. As in newspaper articles, we expect the most important concepts to come first, and we expect them to be 
expressed with the least amount of polluting detail. We expect the low-level details to come last.

## Team Rules
The title of this section is a play on words. Every programmer has his own favorite formatting rules, but if he works 
in a team, then the team rules. A team of developers should agree upon a single formatting style, and then every member 
of that team should use that style. We want the software to have a consistent style. We don’t want it to appear to 
have been written by a bunch of disagreeing individuals.


```java
public class CodeAnalyzer implements JavaFileAnalysis {
    private int lineCount;
    private int maxLineWidth;
    private int widestLineNumber;
    private LineWidthHistogram lineWidthHistogram;
    private int totalChars;
    
    public CodeAnalyzer() {
        lineWidthHistogram = new LineWidthHistogram();
    }
    
    public static List<File> findJavaFiles(File parentDirectory) {
        List<File> files = new ArrayList<File>();
        findJavaFiles(parentDirectory, files);
        return files;
    }
    
    private static void findJavaFiles(File parentDirectory, List<File> files) {
        for (File file : parentDirectory.listFiles()) {
            if (file.getName().endsWith(".java"))
                files.add(file);
            else if (file.isDirectory())
                findJavaFiles(file, files);
        }
    }
    
    public void analyzeFile(File javaFile) throws Exception {
        BufferedReader br = new BufferedReader(new FileReader(javaFile));
        String line;
        while ((line = br.readLine()) != null)
            measureLine(line);
    }
    
    private void measureLine(String line) {
        lineCount++;
        int lineSize = line.length();
        totalChars += lineSize;
        lineWidthHistogram.addLine(lineSize, lineCount);
        recordWidestLine(lineSize);
    }
    
    private void recordWidestLine(int lineSize) {
        if (lineSize > maxLineWidth) {
            maxLineWidth = lineSize;
            widestLineNumber = lineCount;
        }
    }
    
    public int getLineCount() {
        return lineCount;
    }
    
    public int getMaxLineWidth() {
        return maxLineWidth;
    }
    
    public int getWidestLineNumber() {
        return widestLineNumber;
    }
    
    public LineWidthHistogram getLineWidthHistogram() {
        return lineWidthHistogram;
    }
    
    public double getMeanLineWidth() {
        return (double)totalChars/lineCount;
    }
    
    public int getMedianLineWidth() {
        Integer[] sortedWidths = getSortedWidths();
        int cumulativeLineCount = 0;
        for (int width : sortedWidths) {
            cumulativeLineCount += lineCountForWidth(width);
            if (cumulativeLineCount > lineCount/2)
                return width;
        }
        throw new Error("Cannot get here");
    }
    
    private int lineCountForWidth(int width) {
        return lineWidthHistogram.getLinesforWidth(width).size();
    }
    
    private Integer[] getSortedWidths() {
        Set<Integer> widths = lineWidthHistogram.getWidths();
        Integer[] sortedWidths = (widths.toArray(new Integer[0]));
        Arrays.sort(sortedWidths);
        return sortedWidths;
    }
}
```
