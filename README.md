class CreditCardValidator:
    def __init__(self, card_number):
        self.card_number = card_number

    def luhn_algorithm(self):
        digits = [int(x) for x in str(self.card_number)]
        digits.reverse()
        for i in range(1, len(digits), 2):
            digits[i] *= 2
            if digits[i] > 9:
                digits[i] -= 9
        total = sum(digits)
        return total % 10 == 0

    def validate(self):
        card_number = ''.join(filter(str.isdigit, self.card_number))
        if len(card_number) != 16:
            return False
        return self.luhn_algorithm()


card_number = input("Введіть номер картки: ")
validator = CreditCardValidator(card_number)
if validator.validate():
    print("Номер картки валідний!")
else:
    print("Номер картки недійсний.")
