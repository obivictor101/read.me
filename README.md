# Testing.txt
import datetime

class Property:
    def __init__(self, property_type, location, price_per_night, description, max_guests):
        self.property_type = property_type
        self.location = location
        self.price_per_night = price_per_night
        self.description = description
        self.max_guests = max_guests

class Booking:
    def __init__(self, property, guest, check_in_date, check_out_date):
        self.property = property
        self.guest = guest
        self.check_in_date = check_in_date
        self.check_out_date = check_out_date

    def calculate_total_price(self):
        nights = (self.check_out_date - self.check_in_date).days
        return self.property.price_per_night * nights

class Guest:
    def __init__(self, name, email, phone_number):
        self.name = name
        self.email = email
        self.phone_number = phone_number

class RentalApp:
    def __init__(self, properties):
        self.properties = properties
        self.bookings = []

    def search_properties(self, location, check_in_date, check_out_date, max_price):
        available_properties = []
        for property in self.properties:
            if property.location == location and property.price_per_night <= max_price:
                is_available = True
                for booking in self.bookings:
                    if booking.property == property and not (check_in_date >= booking.check_out_date or check_out_date <= booking.check_in_date):
                        is_available = False
                        break
                if is_available:
                    available_properties.append(property)
        return available_properties

    def make_booking(self, property, guest, check_in_date, check_out_date):
        booking = Booking(property, guest, check_in_date, check_out_date)
        self.bookings.append(booking)
        return booking
