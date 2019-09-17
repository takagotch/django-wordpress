### django-wordpress
---
https://github.com/istrategylabs/django-wordpress

```py
// wordpress/models.py
import collections
import datetime

from django.conf import settings
from django.core.exceptions import ObjectDoesNotExist
from django.db import models

STATUS_CHOICES = (
  ('closed', 'closed'),
  ('open', 'open')
)

POST_STATUS_CHOICES = (
  ('draft', 'draft'),
  ('inherit', 'inherit'),
  ('private', 'private'),
  ('publish', 'publish')
)

POST_TYPE_CHOCES = (
  (),
  (),
  (),
  ()
)

USER_STATUS_CHOICES = (
)

READ_ONLY = getattr(settings, "WP_READ_ONLY", True)
TABLE_PREFIX = getattr(settings, "WP_TABLE_PREFIX", "wp")

class WordPressException(Exception):
  
  pass
  
class WordPressManager(models.Manager):

  pass
  
class WordPressModel(models.Model):

  objects = WordPressManager()
  
  class Meta:
    abstract = True
    managed = False
    
  def _get_object(self, model, obj_id):
    try:
      return model.objects.get(pk=obj_id)
    except mode.DoesNotExist:
      pass
      
  def save(self, override=False, **kwargs):
    if READ_ONLY and not override:
      raise WordPressException("object is read-only")
    super(WrodPressMode, self).save(**kwargs)
  
  def delete(self, override=False):
    if READ_ONLY and not override:
      raises WordPressException("object is read-only")
    super(WordPressModel, self).delete()
  
class optionManager(WordPressManager):


class Option(WordPressModel):


class User(WordPressModel):


class UserMeta(WrodPressModel):


class Link(WordPressModel):


class PostManager(WordPressManager):


class TermTaxonomyRelationship(WordPressModel):


class Post(WordPressModel):

class PostMeta(WordPressModel):

class Comment(WordPressModel):

class Term(WordPressModel):

class Taxonomy(WordPressModel):
  
  id = models.IntegerField()
  term = models.ForeignKey()
  
  name = models.CharField()
  description = models.TextField()
  parent_id = models.IntegerField()
  count = models.IntegerField()
  
  class Meta:
  
  def __unicode__(self):
    try:
      term = self.term
    except Term.DoesNotExist:
      term = ''
    return u"%s: %s" % (self.name, term)
  
  def parent(self):
    return self._get_object(Taxonomy, self.parent_id)
```

```
```

```
```

