import json
import requests
from config import currency


class APIException(Exception):
    pass


class CurrencyConverter:
    @staticmethod
    def get_price(quote: str, base: str, amount: str):
        if quote == base:
            raise APIException(f'STOP. Невожможно конвертировать одинаковые валюты "{base}".')

        try:
            quote_ticker = currency[quote]
        except KeyError:
            raise APIException(f'STOP. Не удалось обработать валюту "{quote}".')

        try:
            base_ticker = currency[base]
        except KeyError:
            raise APIException(f'STOP. Не удалось обработать валюту "{base}".')

        try:
            amount = float(amount)
        except ValueError:
            raise APIException(f'STOP. Не удалось обработать количество "{amount}"')

        r = requests.get(f'https://free.currconv.com/api/v7/convert?q={quote_ticker}_{base_ticker}\
&compact=ultra&apiKey=80ee990ac66805c88eb2')
        exchange = json.loads(r.content)
        total_base = round(exchange[f'{quote_ticker}_{base_ticker}'] * amount, 3)

        return total_base
