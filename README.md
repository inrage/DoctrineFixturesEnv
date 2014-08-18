DoctrineFixturesEnv
===================

Loads Doctrine Data Fixtures by environment (prod, dev, test, ...)

Installation (with composer)
----------------------------
composer.json
```js
{
        "require": {
                "inrage/doctrine-fixtures-env": "dev-master"
        },
        "repositories": [
                {
                        "type": "git",
                        "url": "git@github.com:inRage/DoctrineFixturesEnv.git"
                }
        ]
}
```

Now download the bundle:

```bash
$ php composer.phar update inrage/doctrine-fixtures-env
```

Usage
-----

Create your DataFixture

```php
<?php
// src/Acme/DemoBundle/DataFixtures/ORM/LoadDevUsersData.php

namespace Acme\DemoBundle\DataFixtures\ORM;

use Doctrine\Common\Persistence\ObjectManager;
use Acme\DemoBundle\Entity\AcmeItem;
use inrage\DataFixturesEnv\AbstractDataFixture;

class LoadDevUsersData extends AbstractDataFixture
{
    /**
     * Performs the actual fixtures loading.
     *
     * @see \Doctrine\Common\DataFixtures\FixtureInterface::load()
     *
     * @param ObjectManager $manager The object manager.
     */
    protected function doLoad(ObjectManager $manager)
    {
        $item = new AcmeItem();
        $item->setHello('world');

        $this->addReference('hello-world', $item);

        $manager->persist($user);

        $manager->flush();
    }

    /**
     * Returns the environments the fixtures may be loaded in.
     *
     * @return array The name of the environments.
     */
    protected function getEnvironments()
    {
        return array('dev');
    }

    /**
     * Get the order of this fixture
     *
     * @return integer
     */
    public function getOrder()
    {
        return 1;
    }
}

```

Console
-------

```bash
app/console doctrine:fixtures:load --env=prod
app/console doctrine:fixtures:load --env=dev
```
