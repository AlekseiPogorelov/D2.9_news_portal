Команды

## Создать двух пользователей (с помощью метода User.objects.create_user('username')).

user1 = User.objects.create_user(username='Alex')
user2 = User.objects.create_user(username='Vlad')

## Создать два объекта модели Author, связанные с пользователями.

Author.objects.create(authorUser=user1)
Author.objects.create(authorUser=user2)

## Добавить 4 категории в модель Category.

Category.objects.create(name='Sport')
Category.objects.create(name='Politic')
Category.objects.create(name='Economy')
Category.objects.create(name='Society')

## Добавить 2 статьи и 1 новость.

author = Author.objects.get(id=1)
Post.objects.create(author=author, categoryType='AR', title='first', text='sume text')
author = Author.objects.get(id=2)
Post.objects.create(author=author, categoryType='AR', title='second', text='sume text2')
author = Author.objects.get(id=1)
Post.objects.create(author=author, categoryType='NW', title='first NEWS', text='TEXT of the first NEWS')

## Присвоить им категории (как минимум в одной статье/новости должно быть не меньше 2 категорий).

Post.objects.get(id=1).postCategory.add(Category.objects.get(id=1))
Post.objects.get(id=2).postCategory.add(Category.objects.get(id=1))
Post.objects.get(id=2).postCategory.add(Category.objects.get(id=2))
Post.objects.get(id=3).postCategory.add(Category.objects.get(id=3))
Post.objects.get(id=3).postCategory.add(Category.objects.get(id=4))

## Создать как минимум 4 комментария к разным объектам модели Post (в каждом объекте должен быть как минимум один комментарий).

Comment.objects.create(commentPost=Post.objects.get(id=1), commentUser=Author.objects.get(id=1).authorUser, text='TEXT for comment - 1')
Comment.objects.create(commentPost=Post.objects.get(id=1), commentUser=Author.objects.get(id=2).authorUser, text='TEXT for comment - 2')
Comment.objects.create(commentPost=Post.objects.get(id=2), commentUser=Author.objects.get(id=2).authorUser, text='TEXT for comment - 2.1')
Comment.objects.create(commentPost=Post.objects.get(id=3), commentUser=Author.objects.get(id=1).authorUser, text='TEXT for comment - 3.1')
Comment.objects.create(commentPost=Post.objects.get(id=3), commentUser=Author.objects.get(id=2).authorUser, text='TEXT for comment - 3.1')
Comment.objects.create(commentPost=Post.objects.get(id=3), commentUser=Author.objects.get(id=1).authorUser, text='TEXT for comment - 3.3')
Comment.objects.create(commentPost=Post.objects.get(id=3), commentUser=Author.objects.get(id=2).authorUser, text='TEXT for comment - 3.4')

## Применяя функции like() и dislike() к статьям/новостям и комментариям, скорректировать рейтинги этих объектов.

Post.objects.get(id=1).like()
Post.objects.get(id=1).like()
Post.objects.get(id=1).like()
Post.objects.get(id=1).like()
Post.objects.get(id=1).like()
Post.objects.get(id=1).like()
Post.objects.get(id=1).dislike()
Post.objects.get(id=2).like()
Post.objects.get(id=2).like()
Post.objects.get(id=2).like()
Post.objects.get(id=2).like()
Post.objects.get(id=2).like()
Post.objects.get(id=2).dislike()
Post.objects.get(id=2).dislike()
Post.objects.get(id=3).like()
Post.objects.get(id=3).like()
Comment.objects.get(id=1).like()
Comment.objects.get(id=1).like()
Comment.objects.get(id=1).like()
Comment.objects.get(id=2).like()
Comment.objects.get(id=2).like()
Comment.objects.get(id=3).like()
Comment.objects.get(id=4).dislike()
Comment.objects.get(id=5).like()
Comment.objects.get(id=6).like()
Comment.objects.get(id=6).like()
Comment.objects.get(id=7).like()
Comment.objects.get(id=7).like()
Comment.objects.get(id=7).like()
Comment.objects.get(id=7).dislike()
Comment.objects.get(id=7).dislike()

## Обновить рейтинги пользователей.

a = Author.objects.get(id=1)
a.update_rating()
a.authorRating
b = Author.objects.get(id=2)
b.update_rating()
b.authorRating 

## Вывести username и рейтинг лучшего пользователя (применяя сортировку и возвращая поля первого объекта).

Author.objects.order_by('-authorRating')[0].authorUser.username

## Вывести дату добавления, username автора, рейтинг, заголовок и превью лучшей статьи, основываясь на лайках/дислайках к этой статье.

r = Post.objects.order_by('-rating')[0]
r.dateCreation.strftime("%d/%m/%y"), r.author.authorUser.username, r.rating, r.title, r.preview()

## Вывести все комментарии (дата, пользователь, рейтинг, текст) к этой статье.

comm = Comment.objects.filter(commentPost=r.id)
for q in comm:
    print(q.dateCreation.strftime("%d/%m/%y"), q.commentUser.username, q.rating, q.text)
