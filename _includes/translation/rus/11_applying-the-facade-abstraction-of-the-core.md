<!-- ### Использование фасада: абстракция ядра -->

В нашей архитектуре:

{:.message}
Фасад выполняет роль **абстракции** ядра приложения, которая находится между
медиатором и нашими модулями. Фасад, в идеальной ситуации, модули должны
взаимодействовать **только** с фасадом, и не должны ничего знать об остальной
части системы.

В ответственность фасада входит обеспечение **консистентного интерфейса** для
модулей, который доступен в любой момент. Это очень сильно напоминает роль
**контроллера песочницы**, в отличной архитектуре, которую впервые предложил
Николас Закас.

Компоненты взаимодействуют с медиатором посредством фасада, по этому он должен
быть **надежен**. Говоря «взаимодействуют», я должен уточнить, что фасад это
абстракция медиатора, которая слушает сообщения исходящие от модулей, и
передает их обратно медиатору. (???)

В дополнение к предоставлению интерфейса для модулей, фасад так же выступает
как страж безопасности, определяя с какими частями приложения может
взаимодейстовать модуль. Компоненты могут вызывать только **свои собственные**
методы, и не долдны иметь доступ любым к интерфейсам, без специального разрешения.
Например, модуль может отправить сообщение `dataValidationCompletedWriteToDB`.
Идея проверки безопасности заключается в том, чтобы проверить, действительно ли
этот модуль имеет права на запись в базу данных. Таким образом, мы пытаемся
предотвратить проблемы с модулями, которые пытаются делать что-то, что они
делать не должны. 

Подведем итоги: медиатор представляет из себя вариацию основанную на паттерне 
«подписчик/издатель», но он получает только интересующие нас сообщения, которые
проходят проверку на соответсвующие им разрешения в фасаде.