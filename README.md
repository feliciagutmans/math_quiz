# math_quiz

'''
Felicia Gutmans

Msc Computer Science Application, UCL

April 2017

This programme has been designed as a simple maths quizz testing the user on
the Pythagorean theorem. It takes Pythagorian triples and multiplies them up to
seven times, to generate random side lengths of the triangle. These Pythagorian
triples ensure implimentation simplicity and prevent having to chek rounded
decimals. Given two lengths, the user has to calculate the third length. The
user's input is then checked and replied with "correct" if it is the right answer
or "incorrect" if it is the wrong answer. "Correct" answers are allocated one
mark which is added to give the user a score when the user decides to end the
quizz, that is given in a percentage, based on the number of right answers.
'''


import random

def main():

    intro()

    # initialises the counting of right answers and the total number of questions
    # asked
    count =0
    totalQuestions = 0

    # asks user if they want to solve a question or exit
    response = raw_input("Would you like to solve a question? Y/N")

    while (response == "Y"):
        # updates total number of question asked
        totalQuestions = totalQuestions +1

        # gets question data
        question = make_question()
        type = question[0]
        O = question[1]
        A = question[2]
        H = question[3]

        # asks user the question
        value = raw_input(askQuestion(type,O,A,H))

        # checks user's answers, updates count if correct
        count = check_answer(type,int(value),O,A,H,count)

        # asks again
        response = raw_input("Would you like to solve another question? Y/N ")

    # prints score when the user exits.
    get_score(count,totalQuestions)


# defines core question phrases
def askQuestion(type,O,A,H):
    """Define three different types of questions, ask user to calculate one side of
    the triangle given the other two sides and await user input."""
    intro = "Given a right-angled triangle with sides"
    outro = ", calculate the value of "

    # gives user O and A, asks to calculate H
    if type ==  1:
        question = " O=" + str(O) + ", A=" +str(A) + outro + "H."
    # gives user H and A, asks to calculate O
    elif type == 2:
        question = " H=" + str(H) + ", A=" +str(A)+ outro + "O."
    # gives user H and O, asks to calculate A
    elif type == 3:
        question = " O=" + str(O) + ", H=" +str(H)+ outro + "A."
    # returns question
    return intro + question

# verifies that the answer inputted is correct
def check_answer(type,answer,O,A,H,count):
    """Verify the user's input, if it is the right answer, return "Correct" and add
    one mark to the user's score, otherwise return "Incorrect" and add no marks."""
    # defines which question type corresponds to which side
    if (type == 1 and answer == H) or (type == 2 and answer == O) or (type == 3
        and answer == A):
        print("Correct")
        # if the answer is correct, allocates 1 mark
        count = count + 1
        return count
    else:
        print("Incorrect")
        # if the answer is incorrect, allocates no marks
        return count

# calculates the score based on user input
def get_score(numCorrect,totalNum):
    """Calculate the user's percentage score based on the number of inputted
    answers that were correct but return a score of 0% if user did not answer
    any questions. End program and bid user goodbye."""
    print("Your score was: ")
    if totalNum == 0:
        # if no questions were answered prints 0%
        print("0")
    else:
        # calculates score percentage
        print(str((float(numCorrect) / totalNum) * 100))
    print("%")
    # end of programme
    print("Thank you and goodbye.")


def make_question():
    """Define the lengths of the triangle to be 3 for the O, 4 for the A and 5
    for the H, a Pythogorean triple. Define these lengths be multiplicable up to
    seven times, all together, chosen randomly."""
    # generates the minimum side lengths of the triangle
    o_seed=3
    a_seed=4
    h_seed=5

    # randomly generates the side lengths of the triangle from up to seven multiples
    rand_num = random.randint(1,7)
    type = random.randint(1,3)

    #define O, A and H for each side of the triangle, to be featured in question
    O = o_seed * rand_num
    A = a_seed * rand_num
    H = h_seed * rand_num
    return [type, O, A, H]

# prints the introduction statement for the quiz
def intro():
    """Present the programme with a small introductory text."""
    title = "** Solving Pythagoras Quizz, Spring 2017 **"
    print("*" * len(title))
    print(title)
    print("*" * len(title))

main()
