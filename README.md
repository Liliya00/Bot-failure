import json
import datetime




class Dialog:
    def __init__(self):
        self.dialog = []

    def add_message(self, speaker, message):
        self.dialog.append({speaker: message})

    def save_dialog(self, filename):
        with open(filename, 'w') as file:
            json.dump(self.dialog, file)
class BotClass:
    __instance = None

    def __init__(self):
        self.subject = None
        self.dialog = Dialog()
        self.previous_subjects = []

    @staticmethod
    def get_instance():
        if not BotClass.__instance:
            BotClass.__instance = BotClass()
        return BotClass.__instance

    def start_conversation(self):
        while True:
            if self.subject:
                self.subject.process_questions()
            else:
                subject_choice = input('Вітаю, мене звати НЕЗНАЙКО. Ви можете задати мені питання з наступних тем: фізика, математика, географія, Філологія, текст, загальне або "вийти": ')
                if subject_choice.lower() == 'вийти':
                    break
                self.select_subject(subject_choice)
    def select_subject(self, subject_choice):
        if subject_choice.lower() == 'фізика':
            self.subject = Physics()
            self.previous_subjects.append(self.subject)
        elif subject_choice.lower() == 'математика':
            self.subject = Maths()
            self.previous_subjects.append(self.subject)
        elif subject_choice.lower() == 'географія':
            self.subject = Geography()
            self.previous_subjects.append(self.subject)
        elif subject_choice.lower() == 'філологія':
            self.subject = Philology()
            self.previous_subjects.append(self.subject)
        elif subject_choice.lower() == 'текст':
            self.subject = Text()
            self.previous_subjects.append(self.subject)
        elif subject_choice.lower() == 'загальне':
            self.subject = General()
            self.previous_subjects.append(self.subject)
        elif subject_choice.lower() == 'назад':
            if self.previous_subjects:
                self.subject = self.previous_subjects.pop()
                print('Повертаюся до попередньої теми.')
            else:
                print('Немає попередніх тем.')
        else:
            print('Невідомий предмет. Будь ласка, спробуйте ще раз.')

    def save_dialog(self):
        current_time = datetime.datetime.now().strftime("%d-%m-%Y_%H-%M-%S")
        filename = f"dialog-{current_time}.txt"
        self.dialog.save_dialog(filename)

    def load_dialog(self, filename):
        with open(filename, 'r') as file:
            self.dialog = json.load(file)

class Subject:
    def process_questions(self):
        pass

class Physics(Subject):
    def process_questions(self):
        while True:
            question = input('Ви обрали тему "фізика". Ви можете задати  мені питання з наступних тем: закон збереження енергії, закон Бойля - Маріотта. Уведіть ваше питання або "вийти": ')

            self.process_question(question)

    def process_question(self, question):
        if 'закон збереження енергії' in question.lower():
            self.einstein(question)
        elif 'закон бойля - маріотта' in question.lower():
            self.boyles_law(question)
        else:
            print('Я не знаю цієї теми, натомість, ви можете задати мені питання з наступних тем: закон збереження енергії, закон Бойля - Маріотта')
    def einstein(self, question):
        print('Ви обрали тему "Закон збереження енергії".')
        a = input('Уведіть Eкін: ')
        a1 = input('Уведіть Епот: ')
        a2 = input('Уведіть Евнутр: ')
        sum_a = a + a1 + a2
        print('const = ' + sum_a)
    def boyles_law(self, question):
        b = input('Ви хочете обчислити P1 або V1?: ')
        if 'p1' in b.lower():
            b1 = float(input('Уведіть V1: '))
            b11 = float(input('Уведіть V2: '))
            b2 = float(input('Уведіть P2: '))
            bs = b2 * b11 / b1
            print('P1 = ' + bs)
        elif 'v1' in b.lower():
            b3 = float(input('Уведіть V2: '))
            b4 = float(input('Уведіть P1: '))
            b44 = float(input('Уведіть P2: '))
            bs1 = b44*b3 / b4
            print('V1 = ' + bs1)
        else:
            print('Помилка')

class Maths:
    def process_questions(self):
        while True:
            question = input('Ви обрали тему "математика". Ви можете задати  мені питання з наступних тем: найбільший спільний дільник або найменше спільне кратне '
                             'двох чисел, формула скалярного добутку векторів, формула для обчислення довжини відрізка між двома точками на площині, площа трапеці, координати центра кола або "вийти": ')
            if question.lower() == 'вийти':
                break
            self.process_question(question)

    def process_question(self, question):
        if 'найбільший спільний дільник або найменше спільне кратне двох чисел' in question.lower():
            self.nsd_nsk(question)
        elif 'скалярний добуток векторів' in question.lower():
            self.scalar_product(question)
        elif 'обчислення довжини відрізка між двома точками на площині' in question.lower():
            self.segment2(question)
        elif 'площа трапеції' in question.lower():
            self.trapezium(question)
        elif 'координати центру кола' in question.lower():
            self.center(question)
        else:
            print('Я не знаю цієї теми, натомість, ви можете задати мені питання з наступних тем: найбільший спільний дільник або найменше спільне кратне '
                             'двох чисел, формула скалярного добутку векторів, формула для обчислення довжини відрізка між двома точками на площині, площа трапеці, координати центра кола або "вийти": ')
    def nsd_nsk(self, question):
        nsd_nsk = input('Шукаємо НСД чи НСК?: ')
        if nsd_nsk.upper() == 'НСД':
            nsd1 = input('Введіть перше число: ')
            nsd2 = input('Введіть друге число: ')
            print('НСД чисел'+ nsd1 + nsd2)
        elif nsd_nsk.upper() == 'НСК':
            nsk1 = input('Введіть перше число: ')
            nsk2 = input('Введіть друге число: ')
            nsk = nsk1 + nsk2
            print('НСК чисел ' + nsk1 + nsk2)
        else:
            print('Помилка')

    def scalar_product(self, question):
        pass
    def segment2(self, question):
        pass
    def trapezium(self, question):
        pass
    def center(self, question):
        pass

class Geography:
    def process_questions(self):
        while True:
            question = input('Ви обрали тему "географія". Ви можете задати  мені питання з наступних тем: найбільший за площею океан, держава, що має найбільшу кількість озер в світі, знайти координати точки або "вийти": ')
            if question.lower() == 'вийти':
                break
            self.process_question(question)

    def process_question(self, question):
        if 'найбільший за площею океан' in question.lower():
            print('Тихий')
        elif 'держава, що має найбільшу кількість озер в світі' in question.lower():
            print('Канада')
        elif 'знайти координати точки' in question.lower():
            print('Скоро в нашому боті буде доступна функція "Знайти координати точки В (x2, y2), якщо відомо координати точки А (x1, y1) та відстань між ними (d) і напрямок (азимут) від точки А до точки В (θ)"! Дочекайтеся!')
        else:
            print('Я не знаю цієї теми, натомість, ви можете задати мені питання з наступних тем: найбільший океан за площею, держава з найбльшою кількістю озер, координати точки')

class Philology:
    def process_questions(self):
        while True:
            question = input('Ви обрали тему "філологія". Ви можете задати  мені питання з наступних тем: різниця між present simple та present continuous, питальні речення в англійській мові, відмінки в українській мові  або "вийти": ')
            if question.lower() == 'вийти':
                break
            self.process_question(question)

    def process_question(self, question):
        if 'різниця між present simple та present continuous' in question.lower():
            print('Перейдіть за посиланням: https://test-english.com/explanation/a1/present-simple-present-continuous/')
        elif 'питальні речення в англійській мові' in question.lower():
            print('Перейдіть за посиланням: https://test-english.com/grammar-points/a2/asking-questions-in-english/')
        elif 'відмінки в українській мові' in question.lower():
            print('Називний, родовий, давальний, знахідний, орудний, місцевий, кличний')
        else:
            print('Я не знаю цієї теми, натомість, ви можете задати мені питання з наступних тем: різниця між present simple та present continuous, питальні речення в англійській мові, відмінки в українській мові')

class Text(Subject):
    def process_questions(self):
        while True:
            question = input('Ви обрали тему "текст". Ви можете задати  мені питання з наступних тем: підрахувати скільки разів зустрічається слово в тексті, знайти всі слова, що містять певну літеру, '
                             'кількість слів у тексті, перевести текст в верхній регістр, найдовші слова що починаються з голосної, найдовші слова без голосних або "вийти"')
            if question.lower() == 'вийти':
                break
            self.process_question(question)

    def process_question(self, question):
        if 'підрахувати скільки разів зустрічається слово в тексті' in question.lower():
            self.count_word_occurence(question)
        elif 'знайти всі слова, що містять певну літеру' in question.lower():
            self.certain_letter(question)
        elif 'кількість слів у тексті' in question.lower():
            self.overall_count(question)
        elif 'перевести текст в верхній регістр' in question.lower():
            self.capitals(question)
        elif 'найдовші слова що починаються з голосної' in question.lower():
            self.vowels(question)
        elif 'найдовші слова без голосних' in question.lower():
            self.no_vowels(question)
        else:
            print('Я не знаю цієї теми. Можливі теми: підрахувати скільки разів зустрічається слово в тексті, знайти всі слова, що містять певну літеру, кількість слів у тексті, перевести текст в верхній регістр, найдовші слова що починаються з голосної, найдовші слова без голосних')

    def count_word_occurence(self, question):
        pass

    def certain_letter(self, question):
        pass

    def overall_count(self, question):
        pass

    def capitals(self, question):
        pass
    def vowels(self, question):
        pass
    def no_vowels(self, question):
        pass


class General(Subject):
    def process_questions(self):
        while True:
            question = input('Ви обрали тему "загальні". Ви можете задати  мені питання з наступних тем: скільки днів до Нового Року, вгадай число між 1 та 10, сказати надихаючу цитату, привітай з Днем Народження, скажи комплімент або "вийти": ')
            if question.lower() == 'вийти':
                break
            self.process_question(question)

    def process_question(self, question):
        if 'скільки днів до нового року' in question.lower():
            print('Перейди за посиланням та дізнайся! https://stopwatch-timers.com/uk/zvorotniy-vidlik/chas-do-novogo-roku/')
        elif 'вгадай число між 1 та 10' in question.lower():
            random = random.randint(1, 10)
            return random
        elif 'сказати надихаючу цитату' in question.lower():
            print("Неможливо сказати, що саме ти зможеш зробити, поки не спробуєш.")
        elif 'привітай з днем народження' in question.lower():
            print('З Днем народження! Бажаю вам неймовірного щастя, незабутніх моментів і досягнення всіх ваших мрій. Нехай цей день буде початком нового захоплюючого року вашого життя, наповненого радістю, здоров\'ям і безмежними можливостями. Вітаю ще раз!')
        elif 'скажи комплімент' in question.lower():
            print('Ваша присутність робить цей світ кращим місцем.')
        else:
            print('Я не знаю цієї теми. Можливі теми: скільки днів до Нового Року, вгадай число між 1 та 10, сказати надихаючу цитату, привітай з Днем Народження, скажи комплімент або "вийти"')


bot = BotClass.get_instance()
bot.start_conversation()
bot.save_dialog()
