# Observer Method ##############

This method mainly consist of the Observer and Subject. Observer could be anything which can observe (ex. User). And subject could be anything which is going to update its behaviour. So any subject will change the behaviour then Observer will observe the changes of the behaviour of the Subject.  

The observer method is a Behavioral design Pattern which allows you to define or create a subscription mechanism to send the notification to the multiple objects about any new event that happens to the object that they are observing.  

When any change happened to the Subject then Subject will not aware about the Observers activity. That means, they are loosely coupled.

## Advantage

- Open/Closed Principle: Introducing subscriber classes is much easier in Observer method as compared to others without making changes in the client’s code.
- Establishes Relationships: Its really easy to establishes the relationships at the runtime between the objects.
- Description: It carefully describes about the coupling present between the objects and the observer. Hence, there is no need to modify Subject to add or remove observers.

## Disadvantage

- Memory Leakage: Memory leaks caused by Lapsed Listener Problem because of explicit register and unregistering of observers.
- Random Notifications: All the subscribers present gets notification in the random order.
- Risky Implementations: If the pattern is not implemented carefully, there are huge chances that you will end up with large complexity code.

```python
'''
Obeserver Design pattern
'''

class User:  # Observer class
    '''
    User class will act role of observer to subject
    '''
    def __init__(self, name):
        self.name = name

    def update(self, article, blog_writer):
        print(f'For {self.name}, new article {article} by {blog_writer.name} is added')

class BlogWriter:
    '''
    BlogWriter class is useful to blog writer to add new article
    and manage subscribers as well
    '''
    def __init__(self, name):
        self.name = name
        self.__subscribers = []
        self.__articles = [] # Article is the subject

    def add_article(self, article):
        '''
        Add new article and notify subscribers
        '''
        self.__articles.append(article)
        self.notify_subscribers(article)

    def get_articles(self):
        '''
        Get articles written by {self}
        '''
        return self.__articles

    def subscribe(self, subscriber):
        '''
        Add new subscriber to notify on adding article
        '''
        self.__subscribers.append(subscriber)

    def unsubscribe(self, subscriber):
        '''
        User can unsubscribe from further notifications
        '''
        return self.__subscribers.remove(subscriber)

    def subscribers(self):
        '''
        Get subsribers
        '''
        return self.__subscribers

    def notify_subscribers(self, article):
        '''
        Notifying all the subsribers about new addition of an article
        '''
        for sub in self.__subscribers:
            sub.update(article, self)

if __name__ == '__main__':
    blog_writer = BlogWriter('Hardik\'s blog')
    shailaja = User('Shailaja')
    aarav = User('Aarav')
    blog_writer.subscribe(shailaja)
    blog_writer.subscribe(aarav)
    blog_writer.add_article('Article 1')
    blog_writer.unsubscribe(aarav)
    blog_writer.add_article('Article 2')
```