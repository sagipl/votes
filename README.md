=====
DRF Vote
=====

This is extended version of repo [django-vote](https://github.com/Beeblio/django-vote).

DRF Vote is a simple Django Rest Framework app to add ability to like/dislike a model.

=====
How is it different ?
=====

- Modified to work with django rest framework.
- A new feature of disliking an object is added in this version.

Quick start
-----------

1. Add ``'votes'`` to your ``INSTALLED_APPS`` setting like this::

    ```javascript
    INSTALLED_APPS = (
    ...
    'votes',
    )
    ```

2. Run ``python manage.py syncdb`` to create the vote models.


3. Declare vote field to the model you want to vote::

    ```javascript
    from votes.managers import VotableManager
    
    class ArticleReview(models.Model):
        ...
        votes = VotableManager()
    ```
        
4. Include votes url to your urls.py file::
    
    ```javascript
    from rest_framework.routers import DefaultRouter
    
    from votes.api import VoteQueryset
    
    router = DefaultRouter()
    
    urlpatterns += [
        url(r'^api/v1/', include(router.urls)),
    ]
    ```

API
-----------

/up/
==========
Adds a new like or dislike vote to the object

* param: model, id, vote i.e. model=movies&id=359&vote=true
* vote=option[True for up-vote, False for down-vote, None for no-vote]
    ```javascript
    This api is used for both liking and disliking the object.
    Send
    vote=true for like
    vote=false for dislike
    
    ```

/down/
==========
Removes vote to the object

* param: model, id i.e. model=movies&id=359

/exists/
============
Check if the user already voted the object

* param: model, id i.e. model=movies&id=359

/all/
=========
return all instances voted by user

* param: model, id i.e. model=movies&id=359

/count/
=======
Returns the number of votes for the object

* param: model, id i.e. model=movies&id=359

/users/
=======
Returns a list of users who voted and their voting date

* param: model, id i.e. model=movies&id=359

/likes/
=======
Returns the number of likes and dislikes for the object.

* param: model, id i.e. model=movies&id=359
