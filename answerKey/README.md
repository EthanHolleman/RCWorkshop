# Answer key

This folder contains the correct answer to the insulin assembly problem. The correct sequence as a fasta file
is located in `insulinSeq.fasta`.

If you want to easily check your answer just copy and paste the Python code below. Pass your
answer into the function as a string. It will return and print the percent correctness
of your answer (Hamming distance).

```Python
def check_answer(your_answer: str):
    import requests
    answer = ''.join(requests.get(
        'https://raw.githubusercontent.com/EthanHolleman/RCWorkshop/main/answerKey/insulinSeq.fasta'
    ).text.split('\n')[1:-2])
    
    length_diff = abs(len(your_answer) - len(answer))
    max_score = len(answer)
    your_score = 0
    try:
        for i in range(len(answer)):
            if answer[i] != your_answer[i]:
                your_score += 1
    except IndexError:
        pass
    
    final_score = your_score + length_diff
    message = 'You got ' + str(round((1 - (final_score / len(answer)))*100, 2)) + ' % of the sequence correct'
		print(message)
		return message
 ```
