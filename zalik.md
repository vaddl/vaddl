"""
Волошин Вадим 141
Завдання:
1. Запитати у користувача код регіону
2. Отримати ЗВО з вказаного користувачем регіону
3. Зберегти всі дані у файл universities.csv у форматі csv
4. Збережіть ті ж дані у файл universities_<код регіону>.csv, наприклад universities_80.csv
5. Якщо регіон не зі списку доступних, то повідомити про це користувачеві у консолі
Завдання #1
 Назви та EDRPOU в файл EDRPOU.csv
Завдання #2
З формою фінансування Державна
Завдання 3
Ускладніть програму з другого завдання можливістю фільтрування за будь-яким з наявних значень поля
Підказка - сформуйте список всіх значень що зустрічають і дайте користувачеві обрати
"""
import requests
import csv

region = input('Vvedit region code: ')
codes = ['01', '05', '07', '12', '14', '18', '21', '23', '26', '32', '35', '44', '46', '48', '51', '53', '56', '59',
         '61', '63', '65', '68', '71', '73', '74', '80', '85'];
r = region in codes
   if region not in codes:
       print('Vvedit drygiy code: ')
       return get_region()
   else:
        return region

print('finansyvannya;'/n'1)Derjavna'/n '2)Komynalna'/n'3)Pryvatna')
choose = str(input('Obraty odne'))
r = requests.get('https://registry.edbo.gov.ua/api/universities/?ut=1&lc='+region+'&exp=json')
universities: list = r.json()
filtered_data = [{k: row[k] for k in ['university_id', 'post_index']} for row in universities]
filtered_data2 = [{k: row[k] for k in ['university_name', 'university_name_en', 'university_director_post']}
                  for k in ['university_director_post'] for row in universities if row[k] == value1]

with open("universities.csv", mode="w", encoding="UTF-8") as f:
    writer = csv.DictWriqter(f, fieldnames=filtered_data[0].keys())
    writer.writeheader()
    writer.writerows(filtered_data)

with open('universities_' + key + '.csv', mode='w', encoding='UTF-8') as _file:
    writer = csv.DictWriter(_file, fieldnames=filteredData[0].keys())
    writer.writeheader()
    writer.writerows(filteredData)

 main()
