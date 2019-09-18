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

  id = models.IntegerField(db_column='term_id', primary_key=True)
  name = models.CharField(max_length=200)
  slug = models.CharField(max_length=200)
  group = models.IntegerField(default=0, db_column='term_group')
  
  class Meta:
    db_table = '%s_terms' % TABLE_PREFIX
    ordering = ['name']
    managed = False
    
  def __unicode__(self):
    return self.name
    
  @models.permalink
  def get_absolute_url(self):
    return ('wp_archive_term', (self.slug, ))

class Taxonomy(WordPressModel):
  
  id = models.IntegerField(db_column='term_taxonomy_id', primary_key=True)
  term = models.ForeignKey(Term, related_name='taxonomies', blank=True, null=True)
  
  name = models.CharField(max_length=32, db_column='taxonomy')
  description = models.TextField()
  parent_id = models.IntegerField(default=0, db_column='parent')
  count = models.IntegerField(default=0)
  
  class Meta:
    db_table = '%s_term_taxonomy' % TABLE_PREFIX
    ordering = ['name']
    managed = False
  
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

