# dollars
def dollars_to_words(amount):
    # Define word representations for numbers
    units = ['Zero', 'One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine']
    teens = ['Ten', 'Eleven', 'Twelve', 'Thirteen', 'Fourteen', 'Fifteen', 'Sixteen', 'Seventeen', 'Eighteen', 'Nineteen']
    tens = ['', '', 'Twenty', 'Thirty', 'Forty', 'Fifty', 'Sixty', 'Seventy', 'Eighty', 'Ninety']

    # Define place values
    thousands = [''] + ['Thousand', 'Million', 'Billion', 'Trillion']

    if amount == 0:
        return 'Zero Dollars'

    def convert_below_100(num):
        if num < 10:
            return units[num]
        elif num < 20:
            return teens[num - 10]
        else:
            return tens[num // 10] + ('' if num % 10 == 0 else ' ' + units[num % 10])

    def convert_below_1000(num):
        hundred = num // 100
        rest = num % 100
        if hundred == 0:
            return convert_below_100(rest)
        else:
            return units[hundred] + ' Hundred' + ('' if rest == 0 else ' ' + convert_below_100(rest))

    words = ''
    for i in range(len(thousands)):
        if amount % 1000 != 0:
            words = convert_below_1000(amount % 1000) + ' ' + thousands[i] + ' ' + words
        amount //= 1000

    return words.strip() + ' Dollars'

# Example usage:
amount = 1234567
print(dollars_to_words(amount))
