lesshtml
========

## Screenshots

![django-urls screenshot](https://raw.github.com/aliounedia/lesshtml/master/list.JPG "")
![django-urls screenshot](https://raw.github.com/aliounedia/lesshtml/master/dashboard.JPG "")
![django-urls screenshot](https://raw.github.com/aliounedia/lesshtml/master/detail.JPG "")


La probleme a la quelle beaucoup de developpeurs sont  confronté lorsque ils 
doivent mettre en place un site en quelques minutes est le front /HTML
css, image  .En general le  developpeur n'est pas bon dans ses choses la , et 
meme si il s'y colle , le  resultat est en general merdique ( Tres Moche ).

L'alternatif qui s'offre a eux comme l'a dit un fois Jacob Kaplan Moss est 
d'utiliser  l'applications contrib.admin afin de profiter au maximun des aventages
de cette application . L'experience est plutot enrichissante parceque en
realité il est possible pour une developpeur de developper entierrement 
une application sans tapper une seule ligne de code Html .Et dans un 
environnement de production  c'est plutot utile:

Exemple:
Un cas  simple comme celui ci :
lesshtml:
   __init__.py
  admin.py
  forms.py
  views.py

models.py
=========

from django.contrib import admin
from models import Person
class PersonAdmin(admin.ModelAdmin):
    def old_person_column(self):
        if self.age >30:
            column ='<span style="background:#0B6121;" >'\
                    '<a href ="/person/detail/%s">%s</a></span>'%(
                        self.pk , self.name)
        else:
            column = '<span style="background:#DF0101;" >'\
                     '<a href ="/person/detail_old/%s">%s</a></span>'%(
                         self.pk , self.name)
        return column.lower()
    
    old_person_column.short_description ='Person'
    old_person_column.allow_tags        =True

    def africa_contry(self):
        if self.country in ('SENEGAL' , 'MALI', 'MAURITANIE'):
            column = '<a href ="/person/detail_contry/%s">%s</a></span>'%(
                        self.pk , self.country)
        else:
            column = '<a href ="/person/detail_contry/%s">%s</a></span>'%(
                        self.pk , self.country)
        return column.lower()
            
    africa_contry.short_description ='Africa'
    africa_contry.allow_tags         =True


    def name_column(self):
        return self.name.lower()

    def country_column(self):
        return self.country.lower()
        
    list_display = ('pk' , name_column , country_column ,
                    old_person_column ,
                    africa_contry )
    fields = ['name']
    
    class Meta:
        css = {
              'all': (
            'css/person.css',)

        }
        js = (
        'js/person.js',
        
    )
admin.site.register(Person, PersonAdmin)


models.py 
=========

from django.db import models

class Person(models.Model):
      
      name = models.CharField(max_length =20)
      age  = models.IntegerField(default =0)
      country  = models.CharField(max_length = 200)

      def __unicode__(self):
          return u'<Person  |name :%s | Age :%s>' %(self.name, self.age)



On arrive  facile a developper une application  solide en ne faisant de du customisation
.Je suis sure que beaucoup developpeurs voudraient temps soit peu developper tres
rapidement sans etre limités par des integrateurs : ) , ils peuvent nous mener 
la vie difficile ces gens .En tout cas pour moi tout deveolppeur consient du plobleme
devrais reflechir sur l'alternative que nous offre django pour avoir plus de liberte 
de  delirer dans dans le code

Le Barcamp sera une occasion pour nous d'en discuter!

https://github.com/aliounedia/lesshtml
https://github.com/aliounedia

Enjoy
--Ad



## Requirements