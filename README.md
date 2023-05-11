## How is it different from original tool ?
Ans:- I was working on a project, I needed to take output of this tool one by one for further operation. It was not possible with original tool. So, i edited it.

How to save output:
```
python3 censys-subdomain-finder.py {domain} > output.txt
```

# Censys subdomain finder

This is a tool to enumerate subdomains using the Certificate Transparency logs stored by [Censys](https://censys.io). It should return any subdomain who has ever been issued a SSL certificate by a public CA.

See it in action:

```shell
$ python3 censys-subdomain-finder.py github.com

hq.github.com
talks.github.com
cla.github.com
github.com
cloud.github.com
enterprise.github.com
help.github.com
collector-cdn.github.com
central.github.com
smtp.github.com
cas.octodemo.github.com
schrauger.github.com
jobs.github.com
classroom.github.com
dodgeball.github.com
visualstudio.github.com
branch.github.com
www.github.com
edu.github.com
education.github.com
import.github.com
styleguide.github.com
community.github.com
server.github.com
mac-installer.github.com
registry.github.com
f.cloud.github.com
offer.github.com
helpnext.github.com
foo.github.com
porter.github.com
id.github.com
atom-installer.github.com
review-lab.github.com
vpn-ca.iad.github.com
maintainers.github.com
raw.github.com
status.github.com
camo.github.com
support.enterprise.github.com
stg.github.com
rs.github.com

```

## Setup

1) Register an account (free) on https://censys.io/register
2) Browse to https://censys.io/account, and set two environment variables with your API ID and API secret:

    ```shell
    export CENSYS_API_ID=...
    export CENSYS_API_SECRET=...
    ```

    Alternatively, you can use a `.env` file to store these values for persistence across uses:

    ```shell
    cp .env.template .env
    ```

    Then edit the `.env` file and set the values for `CENSYS_API_ID` and `CENSYS_API_SECRET`.

3) Clone the repository:

    ```shell
    git clone https://github.com/christophetd/censys-subdomain-finder.git
    ```

4) Install the dependencies in a virtualenv:

    ```shell
    cd censys-subdomain-finder
    python3 -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
    ```

## Usage

Sample usage:

```shell
python censys-subdomain-finder.py example.com
```

Output the list of subdomains to a text file:

```shell
python censys-subdomain-finder.py example.com -o subdomains.txt
```

```shell
usage: censys-subdomain-finder.py [-h] [-o OUTPUT_FILE]
                                  [--censys-api-id CENSYS_API_ID]
                                  [--censys-api-secret CENSYS_API_SECRET]
                                  domain

positional arguments:
  domain                The domain to scan

optional arguments:
  -h, --help            show this help message and exit
  -o OUTPUT_FILE, --output OUTPUT_FILE
                        A file to output the list of subdomains to (default:
                        None)
  --censys-api-id CENSYS_API_ID
                        Censys API ID. Can also be defined using the
                        CENSYS_API_ID environment variable (default: None)
  --censys-api-secret CENSYS_API_SECRET
                        Censys API secret. Can also be defined using the
                        CENSYS_API_SECRET environment variable (default: None)
```


## Compatibility

Should run on Python 2.7 and 3.5.

## Notes

The Censys API has a limit rate of 120 queries per 5 minutes window. Each invocation of this tool makes exactly one API call to Censys.

Feel free to [open an issue](https://github.com/christophetd/censys-subdomain-finder/issues/new) or to [tweet @christophetd](https://twitter.com/christophetd/) for suggestions or remarks.
