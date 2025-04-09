    вместо NoOpPasswordEncoder используй BCryptPasswordEncoder

Пакет model

    не используй жадную загрузку
    при обновлении и создании нового пользователя могу ввести для поля username значение,  
    которое уже присутствует в БД, в таком случае пользователь не пройдёт аутентификацию. 
    Поле username должно быть уникальным
    переопредели equals и hashCode в entity классах:
https://jpa-buddy.com/blog/hopefully-the-final-article-about-equals-and-hashcode-for-jpa-entities-with-db-generated-ids/

Пакет service

    раздели ответственность класса UserService - создай пакет security, 
    определи класс имплементирующий UserDetailsService в пакете security, 
    а для UserService(Imp) определи интерфейс - этот класс будет отвечать только за бизнес логику
    раздели ответственность метода saveUser, создай отдельный метод для обновления, 
    в котором будешь учитывать бизнес логику при обновлении - проверки существование записи по id, 
    проверку необходимости кодирования пароля
    в методе getUser вместо передачи null в качестве аргумента методу orElse 
    (противоречит использованию Optional), используй orElseThrow и выбрасывай исключение 
    EntityNotFoundException с сообщением (так же в методе deleteUser, в случае отсутвия записи 
    выбрасывай исключение )
