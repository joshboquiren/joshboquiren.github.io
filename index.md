#Assign3-Vigenere-Encode-JJB.py
#Josh Boquiren
#26 October 2017
#A program to input a file, encrypt its content based on the Vigenere method and output the results to a file

from graphics import *
def main():

    win = GraphWin("VigenereEncode-JJB",500,300)
    win.setBackground("grey")
    alpha = "abcdefghijklmnopqrstuvwxyz"
    encrypting = ''
    
#Input file entry
    prompt1 = Text(Point(120,30),"Enter name of file to be encrypted")
    prompt1.draw(win)
    textPoint1 = Point(280,30)
    infile = Entry(textPoint1, 20)
    infile.setFill("white")
    infile.draw(win)
#Key expression entry
    prompt2 = Text(Point(105,70),"Enter a single word to be used as a key")
    prompt2.draw(win)
    textPoint2 = Point(280,70)
    keyIn = Entry(textPoint2,20)
    keyIn.setFill("white")
    keyIn.draw(win)
#Output file entry
    prompt3 = Text(Point(140,110),"Enter name of output file")
    prompt3.draw(win)
    textPoint3 = Point(280,110)
    outfile = Entry(textPoint3,20)
    outfile.setFill("white")
    outfile.draw(win)
#Button
    button = Rectangle(Point(210,190),Point(310,240))
    button.setFill("grey")
    button.draw(win)
    prompt4 = Text(Point(260,215),"Encrypt")
    prompt4.draw(win)
    win.getMouse()
#Converting for functionality
    readFile = infile.getText()
    key = keyIn.getText()
    xFile = outfile.getText()
    infile = open(readFile,"r") #infile opening
    lenKey = len(key)
    lowKey = key.lower()
    outfile = open(xFile, "w") #outfile writing
    
#Processing
    for line in infile.readlines():
        formatedLine = line.lower().replace(' ','').strip('\n')
        encrypting = ''
        for i in range(len(formatedLine)):
            intMessage = int(alpha.find(formatedLine[i])) #int for index
            intKey = int(alpha.find(lowKey[i%lenKey]))
            intAlpha = int(alpha.find(formatedLine[i]))
            encrypting = encrypting + alpha[(intAlpha + intKey)%26]
        #End for i           
        print(encrypting.upper(), file = outfile)                              
    #End for line

#Closing
    outfile.close()    
    encrypted = Text(Point(265,160), "Encryption complete")
    encrypted.draw(win)
    prompt4.setText("Close")
    closeClick = win.getMouse()
    win.close()
    
#End main
main()
