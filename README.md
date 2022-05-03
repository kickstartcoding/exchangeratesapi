New, Updated Exchange Rates API
----------------------------------

So, to get it running on locally and/or Heroku, here are the steps:


1. Clone our fork that has a few patches for version compatibility (Py 3.6, 3.8 and Sanic 2020+) <https://github.com/kickstartcoding/exchangeratesapi/>

2. Create new shell locally:

        pipenv shell
        pipenv install

3. Create a new Heroku app:


        heroku create
        heroku addons:create heroku-postgresql:hobby-dev
        # Add the remote DB url to a local .env file:
        heroku config:get DATABASE_URL -s  > .env

4. Ensure the `.env` file got created correctly:


        cat .env
        # Should see something quite long, starting with: DATABASE_URL=



5. Test locally:


        heroku local

        curl http://localhost:5000/2020-03-05
        # or
        wget -qO - http://localhost:5000/2020-03-05

        # output:
        # {"base":"EUR","date":"2020-03-03","rates":.....


6. Launch to heroku:

        git push heroku master


Troubleshooting dependency installation
----------------------------------------

1. Try also:

        pipenv install --skip-lock
        pip install gino==0.8.7 # Ensure older version of Gino ORM is installed

2. Try instead of "pipenv install" (in fresh venv):

        pip install -r frozen_requirements.txt

