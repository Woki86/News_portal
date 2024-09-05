домашнее задание для SkillFactory

from news.models import Author, Category, Post, Comment

# 2. Создать двух пользователей
user1 = User.objects.create_user('user1', password='password1')
user2 = User.objects.create_user('user2', password='password2')

# 3. Создать двух авторов, связанных с пользователями
author1 = Author.objects.create(user=user1)
author2 = Author.objects.create(user=user2)

# 4. Добавить 4 категории
category1 = Category.objects.create(name='Category 1')
category2 = Category.objects.create(name='Category 2')
category3 = Category.objects.create(name='Category 3')
category4 = Category.objects.create(name='Category 4')

# 5. Добавить 2 статьи и 1 новость
post1 = Post.objects.create(title='Article 1', author=author1)
post2 = Post.objects.create(title='Article 2', author=author2, is_news=True)

# 6. Присвоить категории
post1.categories.add(category1, category2)
post2.categories.add(category3)

# 7. Создать 4 комментария к разным объектам модели Post
comment1 = Comment.objects.create(post=post1, user=user1, text='Комментарий к 1 статье')
comment2 = Comment.objects.create(post=post1, user=user2, text='Комментарий к 1 статье')
comment3 = Comment.objects.create(post=post2, user=user1, text='Комментарий к 2 статье')
comment4 = Comment.objects.create(post=post2, user=user2, text='Комментарий к 2 статье')

# 8. Применить функции like() и dislike() к статьям/новостям и комментариям
post1.like()   # Предполагается, что метод like() существует
post1.dislike()
comment1.like()
comment2.like()

# 9. Обновить рейтинги пользователей
user1.update_rating()  # Предполагается, что такая функция написана
user2.update_rating()

# 10. Вывести username и рейтинг лучшего пользователя
best_user = Author.objects.order_by('-rating').first()
print(best_user.user.username, best_user.rating)

# 11. Вывести данные лучшей статьи
best_post = Post.objects.order_by('-rating').first()
print(best_post.created_at, best_post.author.user.user.username, best_post.rating, best_post.title, best_post.preview)

# 12. Вывести все комментарии к этой статье
comments = Comment.objects.filter(post=best_post)
for comment in comments:
print(comment.created_at, comment.user.username, comment.rating, comment.text)

